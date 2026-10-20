[English](README.md) | [简体中文](README.zh-CN.md)

# LiteMesh

**LiteMesh: An Efficient Quality-Aware Algorithm for Feature-Preserving Triangle Mesh Simplification**

LiteMesh simplifies triangle meshes while preserving geometric features, balancing geometric fidelity, triangle quality, and computational efficiency.

## Project Links

- Project homepage: https://longwuya.github.io/LiteMesh-homepage/
- Code repository: https://github.com/longwuya/LiteMesh

## Requirements and Dependencies

- Windows x64 and a compiler with C++17 support.
- CMake 3.20 or later.
- vcpkg.
- CGAL, Eigen3, and OpenMP.

The repository includes components such as ANN, L-BFGS, and PQP. The current build configuration uses a precompiled ANN library for Windows.

## Build

Run the following commands in PowerShell. Install CMake, vcpkg, and the Visual Studio C++ build tools first, and set the `VCPKG_ROOT` environment variable to your vcpkg installation directory.

```powershell
git clone https://github.com/longwuya/LiteMesh.git
cd LiteMesh

& "$env:VCPKG_ROOT\vcpkg.exe" install --triplet x64-windows

cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake" -A x64
cmake --build build --config Release
```

The CMake target is named `LiteCAD`. The executable is generated at `build/src/Release/LiteCAD.exe`.

## Run

```text
LiteCAD.exe <INPUT> <OUTPUT> <SIZE> <FACTOR_OF_DECAY> <FACTOR_FOR_PARTICLE_SYSTEM>
```

| Parameter | Description |
| --- | --- |
| `INPUT` | Path to the input mesh file. |
| `OUTPUT` | Output directory. |
| `SIZE` | Target number of sample points. |
| `FACTOR_OF_DECAY` | Energy decay factor for the particle system. Recommended value: `0.95`. |
| `FACTOR_FOR_PARTICLE_SYSTEM` | Particle system coefficient. Recommended value: `0.3`. |

Run this example from the repository root:

```powershell
New-Item -ItemType Directory -Path output -Force
.\build\src\Release\LiteCAD.exe .\data\bunny.obj .\output 1000 0.95 0.3
```

Example input meshes are available in `data/`. Results are saved to the specified output directory.
