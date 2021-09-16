# The following lines of boilerplate have to be in your project's
# CMakeLists in this exact order for cmake to work correctly
cmake_minimum_required(VERSION 3.5)

include(FetchContent)
FetchContent_Declare(
        esp-idf
        GIT_REPOSITORY https://github.com/espressif/esp-idf
        GIT_TAG c198f34f4846213bf3d97d263940f67fc7824387
)

FetchContent_GetProperties(esp-idf)
if (NOT esp-idf_POPULATED)
    FetchContent_Populate(esp-idf)
    if (WIN32)
      execute_process(COMMAND "install.ps1" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
      execute_process(COMMAND "export.ps1" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
    else ()
      execute_process(COMMAND "./install.sh" WORKING_DIRECTORY ${esp-idf_SOURCE_DIR})
    endif ()
endif ()

set(ENV{IDF_PATH} ${esp-idf_SOURCE_DIR})
set(ENV{IDF_TARGET} esp32)

include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(hello-world)
