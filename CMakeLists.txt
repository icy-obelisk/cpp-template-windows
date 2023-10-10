cmake_minimum_required(VERSION 3.15)
project(cpp-template)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
include_directories(
    include
)
add_library(
    hello SHARED
    src/hello.cpp
)
add_executable(
    cpp-sample
    src/cpp-sample.cpp
)
target_link_libraries(
    cpp-sample PUBLIC
    hello
)
add_custom_command(
    TARGET cpp-sample POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_BINARY_DIR}/compile_commands.json ${CMAKE_SOURCE_DIR}/
)