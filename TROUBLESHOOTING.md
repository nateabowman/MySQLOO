# Troubleshooting Guide

This guide covers common build issues and their solutions.

## Build Issues

### vcpkg Dependency Installation Fails

**Symptoms:**
- CMake configuration fails with missing package errors
- vcpkg crashes during dependency installation
- PowerShell access errors on Windows

**Solutions:**

1. **Use Visual Studio IDE (Recommended)**
   - Visual Studio has built-in vcpkg integration that handles dependencies more reliably
   - Open the project folder in Visual Studio
   - Select the appropriate CMake preset (windows-x64-release or windows-x86-release)
   - Visual Studio will automatically install dependencies

2. **Update vcpkg**
   ```bash
   git -C ~/vcpkg pull  # Linux
   git -C %USERPROFILE%\vcpkg pull  # Windows
   ```

3. **Manual Dependency Installation**
   - Open the appropriate native tools command prompt (x86 or x64)
   - Run: `vcpkg install openssl:<triplet> libmariadb:<triplet>`
   - Replace `<triplet>` with your target (e.g., `x64-windows-static` or `x86-windows-static`)

### Build Insights Warnings (Windows)

**Symptoms:**
- Warnings about Build Insights in Visual Studio output
- These are warnings only and don't prevent building

**Solution:**
- Disable Build Insights: Tools → Options → Projects and Solutions → VC++ Build Insights → Uncheck "Enable Build Insights"
- Or ignore them - they don't affect the build

### CMake Preset Not Found

**Symptoms:**
- Error: "Preset 'xxx' not found in CMakePresets.json"

**Solution:**
- Ensure you're using the correct preset name
- For Windows: `windows-x64-release` or `windows-x86-release`
- For Linux: `linux-x64-release` or `linux-x86-release`
- Check `CMakePresets.json` for available presets

### Missing Build Tools

**Symptoms:**
- "cmake: command not found"
- "ninja: command not found"

**Solution:**
- Install required build tools:
  - **Linux (Ubuntu/Debian):** `sudo apt install build-essential cmake ninja-build git pkg-config`
  - **Windows:** Install Visual Studio 2022 or later with C++ workload

## Platform-Specific Issues

### Linux Build Issues

**Missing Linux Headers:**
- Error: "openssl requires Linux kernel headers"
- Solution: `sudo apt install linux-libc-dev`

**32-bit Build on 64-bit System:**
- Install multilib packages: `sudo apt install gcc-multilib g++-multilib`

### Windows Build Issues

**Visual Studio Not Found:**
- Ensure Visual Studio 2022 or later is installed
- Install the "Desktop development with C++" workload
- For 32-bit builds, ensure x86 toolchain is installed

**vcpkg Path Issues:**
- Ensure vcpkg is installed at `%USERPROFILE%\vcpkg` (Windows) or `~/vcpkg` (Linux)
- Or set `VCPKG_ROOT` environment variable to your vcpkg location

## Getting Help

If you encounter issues not covered here:

1. Check the main [README.md](README.md) for build instructions
2. Verify all prerequisites are installed
3. Try a clean build (delete `cmake-build-*` directories)
4. Check that your compiler and CMake versions meet requirements

