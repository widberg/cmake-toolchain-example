cmake_minimum_required(VERSION 3.15)

set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/toolchain/build/toolchain.cmake" CACHE STRING "" FORCE)

project(cmake-toolchain-example VERSION 0.0.0 LANGUAGES C)

add_executable(example
	main.c
)
