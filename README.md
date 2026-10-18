# LiteMesh

**LiteMesh: An Efficient Quality-Aware Algorithm for Feature-Preserving Triangle Mesh Simplification**

LiteMesh 面向保留几何特征的三角网格简化，综合考虑几何保真度、三角形质量与计算效率。

## 项目地址

- 项目主页：https://longwuya.github.io/LiteMesh-homepage/
- 代码仓库：https://github.com/longwuya/LiteMesh

## 环境与依赖

- Windows x64 与支持 C++17 的编译器。
- CMake 3.20 或更新版本。
- vcpkg。
- CGAL、Eigen3、OpenMP。

仓库内包含 ANN、L-BFGS 和 PQP 等相关组件。当前构建配置使用 Windows 版 ANN 预编译库。

## 编译

以下命令在 PowerShell 中执行。请先安装 CMake、vcpkg 和 Visual Studio C++ 构建工具，并将 `VCPKG_ROOT` 环境变量设置为 vcpkg 所在目录。

```powershell
git clone https://github.com/longwuya/LiteMesh.git
cd LiteMesh

& "$env:VCPKG_ROOT\vcpkg.exe" install --triplet x64-windows

cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake" -A x64
cmake --build build --config Release
```

当前 CMake 目标名称为 `LiteCAD`，生成的可执行文件位于 `build/src/Release/LiteCAD.exe`。

## 运行

```text
LiteCAD.exe <INPUT> <OUTPUT> <SIZE> <FACTOR_OF_DECAY> <FACTOR_FOR_PARTICLE_SYSTEM>
```

| 参数 | 含义 |
| --- | --- |
| `INPUT` | 输入网格文件路径。 |
| `OUTPUT` | 输出目录。 |
| `SIZE` | 目标采样点数量。 |
| `FACTOR_OF_DECAY` | 粒子系统能量衰减因子，推荐值为 `0.95`。 |
| `FACTOR_FOR_PARTICLE_SYSTEM` | 粒子系统相关系数，推荐值为 `0.3`。 |

在仓库根目录运行示例：

```powershell
New-Item -ItemType Directory -Path output -Force
.\build\src\Release\LiteCAD.exe .\data\bunny.obj .\output 1000 0.95 0.3
```

示例输入网格位于 `data/` 目录，运行结果保存至指定的输出目录。
