cmake_minimum_required(VERSION 3.19)

# Build the toolchain
# This needs to happen at configure time and before the first project call
file(MAKE_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/toolchain/build)
execute_process(
	COMMAND ${CMAKE_COMMAND} .. -G "${CMAKE_GENERATOR}"
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/toolchain/build
	COMMAND_ERROR_IS_FATAL ANY
)
execute_process(
	COMMAND ${CMAKE_COMMAND} --build . --target install
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/toolchain/build
	COMMAND_ERROR_IS_FATAL ANY
)

# Use the built toolchain
set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/toolchain/build/toolchain.cmake" CACHE STRING "" FORCE)

# Now that the toolchain has been setup, we continue as normal
project(cmake-toolchain-example VERSION 0.0.0 LANGUAGES C)

add_executable(example
	main.c
)
