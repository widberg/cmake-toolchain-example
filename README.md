# CMake Toolchain Example

This repository is a simple example of how to use CMake's toolchain functionality to build and use Clang for a Windows target from a foreign host.

For a more complex example that is still easy to understand check out [SerenityOS](https://github.com/SerenityOS/serenity/tree/master/Toolchain).

Note: Using the Visual Studio generator will not work since it [silently ignores the toolchain file settings for CMAKE_C_COMPILER and CMAKE_CXX_COMPILER](https://gitlab.kitware.com/cmake/cmake/-/issues/23385). I recommend using the Ninja generator.

## Getting Started

### Checkout

```sh
git clone https://github.com/widberg/cmake-toolchain-example.git --recursive --shallow-submodules
cd cmake-toolchain-example
```

### Build

You need to re-configure the build from scratch when the toolchain file changes.

```sh
mkdir build
cd build
cmake .. -GNinja
cmake --build .
```

### Run

```sh
D:\cmake-toolchain-example\build>example.exe
Hello, World! (14.0.6 (https://github.com/llvm/llvm-project.git f28c006a5895fc0e329fe15fead81e37457cb1d1))
```

You can see that regardless of which compiler was initially used on the foreign host, the built Clang toolchain was used to compile the executable for Windows.
