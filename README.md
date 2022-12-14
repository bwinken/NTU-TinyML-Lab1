# LAB 1: Deploy Program onto STM32
## Description
In LAB1, we deploy a pretrained sine regression model onto STM32H747. The input of the system is an x value, and the output is computed value of $\sin(x)$.

## Environment Setup
- mbed-cli==1.10.5
- python==3.9
- gcc-arm-none-eabi==9.2.1

1. Install [mbed-cli](https://os.mbed.com/docs/mbed-os/v6.15/build-tools/install-and-set-up.html) by pip (Already done on our server):

    ```
    $ python3 -m pip install mbed-cli
    ```

2. Install [GCC_ARM](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads) by (Already done on our server):
   
    ```
    $ sudo apt-get install gcc-arm-none-eabi
    ```

### Git Pack Download
1. Create folder named `Lab1`

    ```
    $ mkdir Lab1 
    $ cd Lab1
    ```
    
2. Downloaded file from github : 

    ```
    $ git clone https://github.com/marconi1964/tensorflow.git
    ```
    ```
    $ cd tensorflow
    ```


## Build on PC
1. With this command, some necessary libraries and tools will be downloaded. Then test file along with all of its dependencies will be built. Makefile has instructed the C++ compiler to build the code and create a binary, which it will then run. The result should be like this:

    ```
    $ make -f tensorflow/lite/micro/tools/make/Makefile test_hello_world_test
    ```
<p align="center">
    <img src=https://user-images.githubusercontent.com/61946472/184302778-aa919659-94e0-4ce2-9385-87acc595cee3.png>
</p>




## Deploy on STM32H747
Mbed requires source files to be structured in a certain way. The TensorFlow Lite for Microcontrollers Makefile knows how to do this for us, and can generate a directory suitable for Mbed. The building process should be like this:
```
$ make -f tensorflow/lite/micro/tools/make/Makefile TARGET=mbed OPTIMIZED_KERNEL_DIR=cmsis_nn generate_hello_world_mbed_project
```
<!--
![](https://i.imgur.com/tENEHNF.png)
-->
The directory below contains all of the example’s dependencies structured in the correct way for Mbed to be able to build it.
```
$ cd tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed
```


### Setting up Mbed
To get started, use the following command to specify to Mbed that the current directory is the root of an Mbed project:

```
$ python3 -m mbed config root .
```
Next, instruct Mbed to download the dependencies and prepare to build:

```
$ python3 -m mbed deploy
```
<!--
### Modify Mbed Configuration

By default, Mbed will build the project using C++ 98. However, TensorFlow Lite requires C++ 11. Run the following Python snippet to modify the Mbed configuration files so that it uses C++ 11. You should put `modify.py` in `tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed` and enter the command:

`$ python3 modify.py`
-->

### Modify header files

1. Replication `arm_math.h` and `cmsis_gcc.h` to correct folder.

    ```
    $ cd ~/Lab1/tensorflow/
    ```

    ```
    $ cp tensorflow/lite/micro/tools/make/downloads/cmsis/CMSIS/DSP/Include/arm_math.h  tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/mbed-os/cmsis/TARGET_CORTEX_M/arm_math.h
    ```
    ```
    $ cp tensorflow/lite/micro/tools/make/downloads/cmsis/CMSIS/Core/Include/cmsis_gcc.h  tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/mbed-os/cmsis/TARGET_CORTEX_M/cmsis_gcc.h
    ```


### Compile 
1. Go back to right folder :

    ```
    $ cd tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed
    ```
2. To compile, run:

    ```
    $ python3 -m mbed toolchain GCC_ARM
    ```
    ```
    $ python3 -m mbed target DISCO_H747I
    ```
    ```
    $ python3 -m mbed compile -c
    ```
    If successful, you will see the following screen :
    <p align="center">
        <img src=https://user-images.githubusercontent.com/61946472/184845567-0fec5201-88b3-4b80-9bdd-eb4955c3b444.png>
    </p>



3. This will produce a file named `mbed.bin` in `~/Lab1/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/BUILD/DISCO_H747I/GCC_ARM/`. To flash it to the board, copy the file to the volume mounted as a USB drive. For instance:
   
    ```
    $ cp /BUILD/DISCO_H747I/GCC_ARM/mbed.bin /media/<USER>/<BOARD_NAME>/
    ```
    
4. Download Tera Term and Connect with STM32 to see the performance.
<p align="center">
    <img src=https://user-images.githubusercontent.com/61946472/184304013-0ff3c1b5-54e8-48c6-80d4-f906618e994b.png>
</p>

## TODO: Cosine predictor
1. Find `train_hello_world_model.ipynb` in `~/Lab1/tensorflow/tensorflow/lite/micro/examples/hello_world/train`
2. Modify code to cosine predictor, and replace `model.cc`
3. Replace `hello_world_test.cc`provide in our Lab1 Github: 
4. Run the following command to bulid:

    ```
    $ make -f tensorflow/lite/micro/tools/make/Makefile test_hello_world_test
    ```
<p align="center">
    <img src=https://user-images.githubusercontent.com/61946472/184305590-2018128a-3bb1-477e-8605-4c4e1c370fc0.png>
</p>

## TODO [Optional]: Control LCD on STM32H747I
1. Put `BSP` in
    `~/Lab1/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/`
    
2. Put `LCD_DISCO_F746NG.cpp` and `LCD_DISCO_F746NG.h`in
    `~/Lab1/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/tensorflow/lite/micro/examples/hello_world/`

3. Replace `output_handler.cc` in
     `~/Lab1/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/tensorflow/lite/micro/examples/hello_world/output_handler.cc`
     
4. Open `const.cc` and modify it in 
     `~/Lab1/tensorflow/tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed/tensorflow/lite/micro/examples/hello_world/const.cc`
    
    ```
    (Line19) const int kInferencesPerCycle = 10;
    ```
<p align="center">
    <img src=https://user-images.githubusercontent.com/61946472/184305251-4078c8db-0e00-40ec-99aa-c12b2b47af31.gif>
</p>

