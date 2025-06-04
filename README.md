# cmake-presets - Multiarchitecture CMake Presets collection

This repository contains a collection of CMake presets for various architectures and toolchains. These presets simplify the configuration and build process for multiarchitecture projects by providing predefined settings for different platforms.

## 📂 Directory Structure

- **arch/**: Contains architecture-specific presets, such as ARM, x86_64, and AArch64.
- **generator/**: Includes presets for different CMake generators, such as Ninja and Ninja Multi-Config.
- **toolchain/**: Provides toolchain-specific presets for GCC and other compilers.

## ✅ Included Presets

### 🏗️ Architecture-Specific Presets

- **thumbv6m-none-eabi**: ARMv6-M (Thumb, softfp) for bare metal, e.g. Cortex M0, M0+, M1.
- **thumbv7m-none-eabi**: ARMv7-M (Thumb, softfp) for bare metal, e.g. Cortex M3.
- **thumbv7em-none-eabi**: ARMv7e-M (Thumb, softfp) for bare metal, e.g. Cortex M4, M7
- **thumbv7em-none-eabihf**: ARMv7e-M (Thumb, hardfp) for bare metal.
- **thumbv8m.base-none-eabi**: ARMv8-M Baseline (Thumb, softfp) for bare metal, e.g. Cortex M23.
- **thumbv8m.main-none-eabihf**: ARMv8-M Mainline (Thumb, hardfp) for bare metal, e.g. Cortex M33, M35P, M55, M85
- **x86_64-linux-gnu**: x86_64 for Linux.
- **x86_64-windows-gnu**: x86_64 for Windows (MinGW).
- **arm-linux-gnueabihf**: ARMv6 (AArch32) for Linux.
- **aarch64-linux-gnu**: ARMv8-A (AArch64) for Linux.

### ⚙️ Generator Presets

- **ninja**: Ninja, without `CMAKE_BUILD_TYPE` defined.
- **ninja-debug**: Ninja with debug configuration.
- **ninja-release**: Ninja with release configuration.
- **ninja-multi-config**: Ninja Multi-Config generator, without `CMAKE_DEFAULT_BUILD_TYPE` defined.
- **ninja-multi-config-debug**: Ninja Multi-Config generator with default Debug configuration.
- **ninja-multi-config-release**: Ninja Multi-Config generator with default Release configuration.

### 🛠️ Toolchain Presets

- **gcc-arm-none-eabi**: GCC toolchain for AArch32 bare-metal.
- **gcc-arm-none-linux-gnueabihf**: GCC toolchain for AArch32 GNU/Linux with hard floating-point.
- **gcc-x86_64-linux-gnu**: GCC toolchain for x86_64 Linux.
- **gcc-x86_64-w64-mingw32**: GCC toolchain for x86_64 Windows (MinGW).
- **gcc-native**: GCC toolchain for native builds on the host system.
- **gcc-pedantic-warnings**: GCC toolchain with strict pedantic warnings enabled for code quality enforcement.

## 🚀 Usage

1. Include the desired preset file in your `CMakePresets.json` file.
2. Use the `configurePresets` and `buildPresets` defined in the included files to configure and build your project.

### Example

```json
{
    "version": 6,
    "include": [
        "arch/thumbv7m-none-eabi.json",
        "generator/ninja-multi-config.json"
    ],
    "configurePresets": [
        {
            "name": "my-config",
            "inherits": [
                "ninja-multi-config-debug",
                "thumbv7m-none-eabi",
                "gcc-pedantic-warnings"
            ],
            "cacheVariables": {
                "MY_CUSTOM_VARIABLE": "value"
            }
        }
    ],
    "buildPresets": [
        {
            "name": "my-build",
            "configurePreset": "my-config"
        }
    ]
}
```

This example demonstrates how to combine multiple presets, such as a generator preset (`ninja-multi-config-debug`), an architecture preset (`thumbv7m-none-eabi`), and a toolchain preset (`gcc-pedantic-warnings`). 

## License 📜

This project is licensed under the MIT License. See the LICENSE file for details.
