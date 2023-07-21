# cuda-debayer-cmake

Revive the [cuda-debayer project](https://github.com/avionic-design/cuda-debayer) using CMake.

## Modern CMake and CUDA

See https://github.com/CLIUtils/modern_cmake

## Requirements

- cmake version >= 3.18 (when using nvcc)
- cmake version >= 3.22 (when using nvc++/nvhpc compiler)
- cuda toolkit

## How to build with nvcc ?

```bash
# set default CUDA flags passed to nvcc (Nvidia compiler wrapper)
# at least one hardware architecture flags
export CUDAFLAGS="-arch=sm_75 --expt-extended-lambda"
mkdir build
cd build
cmake ..
make
# then you can run the application
./debayer
```

If you use cmake version >= 3.18, here is a slightly updated version using CMAKE_CUDA_ARCHITECTURE
to pass information about actual GPU hardware target architecture:

```bash
# set default CUDA flags passed to nvcc (Nvidia compiler wrapper)
# at least one hardware architecture flags
export CUDAFLAGS="--expt-extended-lambda"
mkdir build
cd build
cmake -DCMAKE_CUDA_ARCHITECTURES="75" ..
make
# then you can run the application
./debayer
```
# How to build with nvc++ (from nvhpc) ?

```bash
# Warning, cmake 3.22.0 required
export CUDAFLAGS="--expt-extended-lambda"
export CXX=nvc++
mkdir build
cd build
cmake -DCMAKE_CUDA_HOST_COMPILER=nvc++ -DCMAKE_CUDA_ARCHITECTURES="75" ..
make
# then you can run the application
./debayer
```
