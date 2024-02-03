<p align="center">
    <img src="https://github.com/WarEagle451/Mythos/blob/master/mythos/resources/branding/logo-name.png">
</p>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/WarEagle451/Blue/blob/master/LICENSE)

# Table of Contents
1. [Requirements](#requirements)
2. [Libraries](#3rd-party-libraries)
3. [Getting Started](#getting-started)
4. [Building Mythos](#building-mythos)
5. [Common Issues](#common-issues)

# Requirements
- C++20
- [Python 3.11](https://www.python.org/downloads)
- [Ninja 1.11.1](https://github.com/ninja-build/ninja/releases/tag/v1.11.1)
- [LLVM 17.0.1](https://github.com/llvm/llvm-project/releases/tag/llvmorg-17.0.1)
- [cmake 3.28.0](https://cmake.org/download/)

# 3rd Party Libraries

# Getting Started
1. Nativate to `Mythos/scripts` and run setup. If needed the python file can also be ran manually, however submodules should be updated and initialized beforehand.
2. Accept any downloads or instructions the setup script requests, URLs are located in the respective `setup_**.py` files in the `Mythos/scripts/python` directory.
3. Mythos should now be ready to be built and compiled.

# Building Mythos
1. Run cmake and select your desired [configuration](https://github.com/WarEagle451/Mythos/blob/master/CMakePresets.json). If the build fails see [Common Issues](#common-issues)
2. The executable will be located in `Mythos/bin/{configuration}`.

# Common Issues
#### `CMAKE_MT-NOTFOUND`
If the build failed due to `CMAKE_MT-NOTFOUND` this is because CMake could not find the manifest tool. This is likely to occur when attempting to build for Windows with Clang.

On Windows this can possibly be solved by one of the following methods;
1. Running vcvarsall.bat.
2. Adding the parent directory of the manifest tool (mt.exe) to the `PATH` system enviromental variable.
3. Manually setting `CMAKE_MT` in a CMakeUserPresets.json file (See below). The manifest tool should be located in `"C:/Program Files (x86)/Windows Kits/10/bin/{WINDOWS SDK VERSION}/x64"`
<details><h4><summary>CMakeUserPresets.json Example File</h4></summary>

```
{
    "version": 8,
    "cmakeMinimumRequired": {
        "major": 3,
        "minor": 28,
        "patch": 0
    },
    "configurePresets": [
        {
            "name": "user-common",
            "hidden": true,
            "cacheVariables": {
                "CMAKE_MT": "C:/Program Files (x86)/Windows Kits/10/bin/10.0.19041.0/x64/mt.exe"
            }
        },
        {
            "name": "override-windows-clang-release-x64",
            "displayName": "Override: Windows x64 Release - Clang",
            "description": "Target Windows with Clang for a x64 Release build",
            "inherits": [ "windows-clang-release-x64", "user-common" ]
        },
        {
            "name": "override-windows-clang-debug-x64",
            "displayName": "Override: Windows x64 Debug - Clang",
            "description": "Target Windows with Clang for a x64 debug build",
            "inherits": [ "windows-clang-debug-x64", "user-common" ]
        },
        {
            "name": "override-windows-clang-dev_release-x64",
            "displayName": "Override: Windows x64 Developer Release - Clang",
            "description": "Target Windows with Clang for a x64 developer release build",
            "inherits": [ "windows-clang-dev_release-x64", "user-common" ]
        }
    ]
}
```
</details>
