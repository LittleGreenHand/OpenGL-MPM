cmake_minimum_required(VERSION 3.20)

project(OpenGL-MPM LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

add_subdirectory(shaders)

add_subdirectory(thirdparty)

add_subdirectory(src)

set_property(DIRECTORY PROPERTY VS_STARTUP_PROJECT OpenGL-MPM)
