# The following lines of boilerplate have to be in your project's
# CMakeLists in this exact order for cmake to work correctly
cmake_minimum_required(VERSION 3.5)

message(STATUS "Hello World - FetchContent_Declare esp-idf")
include(FetchContent)
FetchContent_Declare(
        esp-idf
        GIT_REPOSITORY https://github.com/espressif/esp-idf
        GIT_TAG c198f34f4846213bf3d97d263940f67fc7824387
)

message(STATUS "Hello World - FetchContent_GetProperties esp-idf")
FetchContent_GetProperties(esp-idf)
if (NOT esp-idf_POPULATED)
    message(STATUS "Hello World - FetchContent_Populate esp-idf")
    FetchContent_Populate(esp-idf)
    if (WIN32)
        message(STATUS "Hello World - install dependencies for Windows")
        execute_process(COMMAND "install.bat" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
        execute_process(COMMAND "export.bat" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
#        set(CMAKE_C_COMPILER $ENV{HOME}/.espressif/tools/xtensa-esp32-elf/esp-2020r3-8.4.0/xtensa-esp32-elf/bin/xtensa-esp32-elf-gcc.exe)
#        set(CMAKE_CXX_COMPILER $ENV{HOME}/.espressif/tools/xtensa-esp32-elf/esp-2020r3-8.4.0/xtensa-esp32-elf/bin/xtensa-esp32-elf-g++.exe)
    else ()
        message(STATUS "Hello World - install dependencies for MacOS/Linux")
        execute_process(COMMAND "./install.sh" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
        execute_process(COMMAND "./export.sh" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
    endif ()
endif ()

message(STATUS "Hello World - Set up dependencies")
set(ENV{IDF_PATH} ${esp-idf_SOURCE_DIR})
set(ENV{IDF_TARGET} esp32)

message(STATUS "Hello World - include project.cmake")
include($ENV{IDF_PATH}/tools/cmake/project.cmake)

message(STATUS "Hello World - project")
project(hello-world)
