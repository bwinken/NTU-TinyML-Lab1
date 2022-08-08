cmake_minimum_required(VERSION 3.21.0)



target_sources(${PROJECT_NAME}
	PUBLIC
		 otm8009a/otm8009a.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 otm8009a
)

target_sources(${PROJECT_NAME}
	PUBLIC
		 ft6x06/ft6x06.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 ft6x06
)

target_sources(${PROJECT_NAME}
	PUBLIC
		 wm8994/wm8994.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 wm8994
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 mt25tl01g
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 Common
)

target_sources(${PROJECT_NAME}
	PUBLIC
		 ov9655/ov9655.c
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		 ov9655
)