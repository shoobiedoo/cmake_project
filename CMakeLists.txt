cmake_minimum_required(VERSION 3.25.2)

project(CMAKE_FIRST)

add_executable(${PROJECT_NAME} main.cpp)
add_subdirectory(Adder)

#Download all the submodules
find_package(Git QUIET)
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
#Update submodules as needed
    option(GIT_SUBMODULES "Check git submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init --recursive command failed with ${GIT_SUBMOD_RESULT} please check")
        endif()
    endif()
endif()
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/external/glfw/CMakeLists.txt")
message(FATAL_ERROR "git submodules are not added as GIT_SUBMODULE might be turned off. Please check and try again")
endif()








add_subdirectory(external/glfw)
target_include_directories(${PROJECT_NAME} PUBLIC Adder  PUBLIC external/glfw/include) # so that in our main file we dont have to inlcude the path for including the header file of the library
target_link_directories(${PROJECT_NAME} PRIVATE Adder  PRIVATE external/glfw/src) #is where are libraries are going to be in the build file
target_link_libraries(${PROJECT_NAME} adder_lib glfw)#links that library with our project