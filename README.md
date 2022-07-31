# LAB 1: Deploy Program onto STM32
### Description
In LAB1, we deploy a pretrained sine regression model onto STM32H747. The input of the system is an x value, and the output is computed value of $\sin(x)$.

### Environment Setup
- mbed-cli==1.10.5
- python==3.9
- gcc-arm-none-eabi==9.2.1

Install the first three by pip. The last one could be installed by:

`$ apt-get install gcc-arm-none-eabi`

### Git Pack Download
Downloaded file would be stored in folder named $Lab1$

`$ mkdir Lab1 && cd "$_"`

`$ git clone https://github.com/marconi1964/tensorflow.git`

`$ cd tensorflow`


### Build on PC
With this command, some necessary libraries and tools will be downloaded. Then test file along with all of its dependencies will be built. Makefile has instructed the C++ compiler to build the code and create a binary, which it will then run. The result should be like this:
    
`$ make -f tensorflow/lite/micro/tools/make/Makefile test_hello_world_test`

![](https://i.imgur.com/56qXKtP.png)

### Fetch CMSIS Pack
`$ make -f tensorflow/lite/micro/tools/make/Makefile TARGET=mbed OPTIMIZED_KERNEL_DIR=cmsis_nn generate_hello_world_mbed_project`

Mbed requires source files to be structured in a certain way. The TensorFlow Lite for Microcontrollers Makefile knows how to do this for us, and can generate a directory suitable for Mbed. The building process should be like this:

![](https://i.imgur.com/tENEHNF.png)
The directory below contains all of the example’s dependencies structured in the correct way for Mbed to be able to build it.

`$ cd tensorflow/lite/micro/tools/make/gen/mbed_cortex-m4_default/prj/hello_world/mbed`



### Setting up Mbed
To get started, use the following command to specify to Mbed that the current directory is the root of an Mbed project:

`$ mbed config root .`
    
Next, instruct Mbed to download the dependencies and prepare to build:

`$ mbed deploy`


