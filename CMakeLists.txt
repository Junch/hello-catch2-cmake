cmake_minimum_required(VERSION 3.5)

project(hello-catch2-cmake LANGUAGES CXX VERSION 0.0.1)
set(CMAKE_CXX_FLAGS "-std=c++17 -Wall")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

include_directories("${PROJECT_SOURCE_DIR}/src")
file(GLOB_RECURSE lib_SOURCES "src/*.cpp" "src/*/*.cpp")
add_library(fibonacci SHARED ${lib_SOURCES})

file(GLOB_RECURSE test_SOURCES "test/*.cpp")
add_executable(hello-catch2-cmake-test ${test_SOURCES})
target_include_directories(hello-catch2-cmake-test PRIVATE "${PROJECT_SOURCE_DIR}/test")
target_link_libraries(hello-catch2-cmake-test fibonacci)

enable_testing()

add_test(
    NAME catch_test
    COMMAND $<TARGET_FILE:hello-catch2-cmake-test> --success
)