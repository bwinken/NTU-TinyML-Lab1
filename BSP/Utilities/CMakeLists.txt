cmake_minimum_required(VERSION 3.21.0)



target_sources(${PROJECT_NAME}
	PUBLIC
		 Fonts/font12.c
		 Fonts/font16.c
		 Fonts/font20.c
		 Fonts/font24.c
		 Fonts/font8.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 Fonts
)