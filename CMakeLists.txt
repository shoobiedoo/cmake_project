cmake_minimum_required(VERSION 3.25.2)

project(CMAKE_FIRST)

add_executable(${PROJECT_NAME} main.cpp)
add_subdirectory(Adder)
target_include_directories(${PROJECT_NAME} PUBLIC Adder) # so that in our main file we dont have to inlcude the path for including the header file of the library
target_link_directories(${PROJECT_NAME} PRIVATE Adder) #is where are libraries are going to be in the build file
target_link_libraries(${PROJECT_NAME} adder_lib)#links that library with our project