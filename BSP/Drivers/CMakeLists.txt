cmake_minimum_required(VERSION 3.21.0)

add_subdirectory(./BSP)


target_include_directories(${PROJECT_NAME}
	PUBLIC
		 BSP
)