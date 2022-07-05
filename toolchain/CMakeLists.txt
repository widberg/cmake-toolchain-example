cmake_minimum_required(VERSION 3.19)

project(cmake-toolchain-example-toolchain VERSION 0.0.0)

# Build the toolchain in Release and install it to the binary directory
set(CMAKE_BUILD_TYPE Release CACHE STRING "")
set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_BINARY_DIR}/install CACHE STRING "" FORCE)
install(DIRECTORY DESTINATION ${CMAKE_INSTALL_PREFIX})

# LLVM
set(LLVM_TARGETS_TO_BUILD "X86" CACHE STRING "")
set(LLVM_ENABLE_PROJECTS "llvm;clang;lld" CACHE STRING "")

set(LLVM_ENABLE_BINDINGS OFF CACHE BOOL "")
set(LLVM_INCLUDE_BENCHMARKS OFF CACHE BOOL "")
set(LLVM_BUILD_UTILS ON CACHE BOOL "")
set(LLVM_INCLUDE_TESTS OFF CACHE BOOL "")
set(LLVM_BUILD_LLVM_DYLIB OFF CACHE BOOL "")
set(LLVM_LINK_LLVM_DYLIB OFF CACHE BOOL "")
set(LLVM_INSTALL_UTILS ON CACHE BOOL "")
set(LLVM_INSTALL_TOOLCHAIN_ONLY OFF CACHE BOOL "")
set(LLVM_INSTALL_BINUTILS_SYMLINKS OFF CACHE BOOL "")
set(CLANG_ENABLE_CLANGD OFF CACHE BOOL "")

set(LLVM_TOOLCHAIN_TOOLS
        llvm-addr2line
        llvm-ar
        llvm-dlltool
        llvm-mt
        llvm-nm
        llvm-objcopy
        llvm-objdump
        llvm-ranlib
        llvm-readelf
        llvm-strip
        CACHE STRING "")

set(LLVM_TOOLCHAIN_UTILITIES
        FileCheck
        CACHE STRING ""
)

add_subdirectory(llvm-project/llvm)

# Toolchain File
configure_file(toolchain.cmake.in ${CMAKE_CURRENT_BINARY_DIR}/toolchain.cmake @ONLY)
