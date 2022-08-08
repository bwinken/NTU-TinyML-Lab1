cmake_minimum_required(VERSION 3.21.0)

add_subdirectory(./Components)


target_include_directories(${PROJECT_NAME}
	PUBLIC
		 Components
)

target_sources(${PROJECT_NAME}
	PUBLIC
		 STM32H747I-Discovery/stm32h747i_discovery_audio.c
		 STM32H747I-Discovery/stm32h747i_discovery.c
		 STM32H747I-Discovery/stm32h747i_discovery_camera.c
		 STM32H747I-Discovery/stm32h747i_discovery_lcd.c
		 STM32H747I-Discovery/stm32h747i_discovery_qspi.c
		 STM32H747I-Discovery/stm32h747i_discovery_sd.c
		 STM32H747I-Discovery/stm32h747i_discovery_sdram.c
		 STM32H747I-Discovery/stm32h747i_discovery_ts.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 STM32H747I-Discovery
)