# CMake Toolchain Example

This repository is a simple example of how to use CMake's toolchain functionality to build and use Clang for a Windows target from a foreign host.

For a more complex example that is still easy to understand check out [SerenityOS](https://github.com/SerenityOS/serenity/tree/master/Toolchain).

## Getting Started

### Checkout

```sh
git clone https://github.com/widberg/cmake-toolchain-example.git --recursive --shallow-submodules
cd cmake-toolchain-example
```

### Build

```sh
# First, we build the toolchain
# You only need to do this the first time and when the toolchain changes
mkdir toolchain/build
cd toolchain/build
cmake .. -GNinja
cmake --build . --target install
cd ../..

# Finally, we build the project
# You will need to re-generate the project when the toolchain changes
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
