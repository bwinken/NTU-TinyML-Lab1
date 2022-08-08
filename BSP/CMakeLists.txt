cmake_minimum_required(VERSION 3.21.0)

add_subdirectory(./Drivers)
add_subdirectory(./Utilities)


target_include_directories(${PROJECT_NAME}
	PUBLIC
		 Utilities
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 Drivers
)