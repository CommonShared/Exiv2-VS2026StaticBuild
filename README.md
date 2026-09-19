# Exiv2 — Visual Studio 2026 Static Build

这是基于最新版本 **Exiv2** 的 Windows 静态编译版本。

本项目使用 **Visual Studio 2026** 构建，并采用 MSVC 静态运行库进行编译，方便在 Windows C++ 项目中直接集成和部署。

## ✨ 构建特点

- **Exiv2**：最新版本
- **Compiler**：Microsoft Visual C++
- **IDE**：Visual Studio 2026
- **Platform**：Windows x64
- **Runtime**：静态运行库
- **Release**：`/MT`
- **Debug**：`/MTd`
- **Architecture**：x64
- **Build Type**：Static Library
- **Language**：C++

使用 `/MT` 和 `/MTd` 后，C/C++ Runtime Library 会静态链接到目标程序中，可以减少最终程序对对应 MSVC Runtime DLL 的依赖。

## 📦 目录结构

```text
Exiv2/
├── include/        # Exiv2 头文件
├── lib/            # 静态库
├── bin/            # 构建后的工具
├── examples/       # 示例
├── CMakeLists.txt
└── README.md
```

具体目录结构可能会根据构建配置有所不同。

## 🔧 编译环境

### Visual Studio

```text
Visual Studio 2026
MSVC
x64
```

### Runtime Library

Release：

```text
/MT
```

Debug：

```text
/MTd
```

对应 Visual Studio：

```text
C/C++ → Code Generation → Runtime Library
```

设置为：

```text
Multi-threaded (/MT)
```

或：

```text
Multi-threaded Debug (/MTd)
```

## 🚀 使用

如果你的 Windows C++ 项目同样使用 MSVC，可以直接将本项目生成的 Exiv2 静态库和头文件集成到自己的工程中。

例如：

```cpp
#include <exiv2/exiv2.hpp>

int main()
{
    auto image = Exiv2::ImageFactory::open("test.jpg");

    if (!image)
        return 1;

    image->readMetadata();

    const Exiv2::ExifData& exif = image->exifData();

    for (const auto& entry : exif)
    {
        std::cout
            << entry.key()
            << " = "
            << entry.value()
            << std::endl;
    }

    return 0;
}
```

> 实际 API 使用方式请以当前 Exiv2 版本的官方文档和头文件为准。

## 🖥️ 适用场景

这个版本主要面向 Windows C++ 开发者，适合用于：

- 图片 Metadata 工具
- EXIF 编辑器
- 图片信息查看器
- 摄影工作流工具
- 图片批处理工具
- Windows 桌面应用
- C++ 图像处理软件
- 自己的商业软件项目

例如：

```text
JPEG
TIFF
PNG
WebP
HEIF
RAW
```

等图像文件的 Metadata 读取和处理。

具体格式支持以当前 Exiv2 版本为准。

## 📌 为什么使用静态运行库？

Windows C++ 应用使用 `/MT` 编译时，MSVC Runtime 会静态链接到程序中。

相比 `/MD`：

```text
/MD
  ↓
依赖 MSVC Runtime DLL
```

使用：

```text
/MT
  ↓
Runtime 静态链接
  ↓
减少运行时 DLL 依赖
```

这对于希望制作独立 Windows 应用程序、减少运行环境依赖的项目比较方便。

需要注意的是，`/MT` 并不意味着所有第三方依赖都会自动静态链接。最终程序是否还依赖其他 DLL，仍然取决于 Exiv2 的具体构建选项以及其依赖库。

## ⚠️ ABI 注意事项

如果你的项目也是使用 MSVC 静态运行库，建议保持一致的运行库配置。

例如：

```text
Application
    │
    ├── /MT
    │
    └── Exiv2
          └── /MT
```

Debug 构建：

```text
Application
    │
    ├── /MTd
    │
    └── Exiv2
          └── /MTd
```

不要随意混用：

```text
Application → /MD
Exiv2       → /MT
```

尤其是在跨模块传递 STL、CRT 所管理的内存、文件句柄等资源时，应特别注意运行库和 ABI 的一致性。

## 🛠️ 自行构建

如果希望自行重新编译，可以使用 CMake + Visual Studio。

Release：

```bash
cmake -S . -B build ^
  -G "Visual Studio 18 2026" ^
  -A x64

cmake --build build --config Release
```

然后根据项目的 CMake 配置，将 MSVC Runtime 设置为静态运行库。

核心配置：

```text
Release → /MT
Debug   → /MTd
```

## 📄 License

Exiv2 本身的许可证、版权信息以及第三方组件许可证，请以 Exiv2 官方项目当前版本所附带的 LICENSE / COPYING 文件为准。

本仓库提供的是针对 Windows / Visual Studio 2026 的构建版本，不改变 Exiv2 原项目的许可证及版权归属。

## 🔗 Upstream

Exiv2 是一个用于读取、写入和管理图像 Metadata 的开源 C++ 项目。

本仓库主要提供：

```text
Exiv2
+
Visual Studio 2026
+
Windows x64
+
Static Runtime (/MT, /MTd)
```

的构建结果，方便 Windows C++ 开发者直接使用。

---

## ⭐ 如果这个构建版本对你的项目有帮助

欢迎 Star ⭐

如果你在 Windows + MSVC 环境中使用 Exiv2，也欢迎提交 Issue 分享构建或集成过程中遇到的问题。