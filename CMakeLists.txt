cmake_minimum_required(VERSION 3.16)
project(cpp-rwlock VERSION 1.0.0 LANGUAGES CXX)

# Set C++20 standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define the header-only library
add_library(${PROJECT_NAME} INTERFACE)

# Specify the include directories for the library
target_include_directories(${PROJECT_NAME} INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>  # for when installed
)

add_subdirectory(example)
