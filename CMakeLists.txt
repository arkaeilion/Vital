cmake_minimum_required(VERSION 3.20.0 FATAL_ERROR)
cmake_policy(VERSION 3.20)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include(${CMAKE_TOOLCHAIN_FILE})

project(Vital VERSION 0.1.0)

file(GLOB VITAL_SRC "src/*.h" "src/*.cpp")
add_executable(${PROJECT_NAME} ${VITAL_SRC})

find_package(sdl2 REQUIRED)
find_package(glm REQUIRED)
find_package(spdlog REQUIRED)
find_package(imgui REQUIRED)
find_package(glad REQUIRED)
find_path(STB_INCLUDE_DIRS "stb_image.h")
find_library(INIH_LIBRARY inih)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		"${CMAKE_CURRENT_SOURCE_DIR}/src/"
        ${SDL2_INCLUDE_DIRS}
        ${GLM_INCLUDE_DIRS}
        ${SPDLOG_INCLUDE_DIRS}
        ${IMGUI_INCLUDE_DIRS}
        ${STB_INCLUDE_DIRS}
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
		SDL2::SDL2
		SDL2::SDL2main
		glm::glm
		spdlog::spdlog
		imgui::imgui
		glad::glad
		${INIH_LIBRARY}
)
