# 🧩 OpenROAD Installation

OpenROAD (Open Runtime for Open Access Design) is an open-source physical design automation (PDA) tool that enables a fully autonomous RTL-to-GDSII flow. It integrates multiple tools like placement, routing, clock tree synthesis, and optimization under one framework.

## 📂 System Requirements

Before installing, make sure your system has:
- OS: Ubuntu 20.04 / 22.04 (recommended)
- RAM: ≥ 16 GB (32 GB preferred)
- Disk: ≥ 50 GB free space
- Tools: git, cmake, make, gcc/g++, python3

## Clone Repository
The first step, independent of the build method, is to download the repository:
```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD.git
cd OpenROAD
```
- The --recursive flag ensures that all submodules (additional repositories within OpenROAD such as OpenSTA, TritonRoute, etc.) are also cloned.
- cd OpenROAD moves into the project directory where all further setup steps will be performed.

## Install Dependencies
```
sudo ./etc/DependencyInstaller.sh -base
./etc/DependencyInstaller.sh -common -local
```
OpenROAD depends on many open-source libraries for compilation and execution (like Boost, Eigen, Tcl, and OpenMP).
- The DependencyInstaller.sh script automatically installs these packages.
- base installs system-level packages that require superuser permissions.
- common -local installs common libraries and Python packages needed locally for OpenROAD modules.
This ensures all required software components are available for the build process.

## Build OpenROAD
```
mkdir build
cd build
cmake ..
```
![WhatsApp Image 2025-11-03 at 11 45 48 AM](https://github.com/user-attachments/assets/a7286747-c0a4-43ca-8f8f-0f15a615e1ee)

CMake is a build automation tool that configures and generates makefiles for compiling the code.
- mkdir build creates a separate directory for the compiled binaries and build files, keeping the source directory clean.
- cmake .. scans the source code (in the parent directory) and prepares a Makefile with the correct build configuration (paths, compiler options, and linked libraries).

## Compile and Install
```
make
sudo make install
```
- The make command compiles the entire OpenROAD project according to the generated Makefile. This process builds all binaries and links the required libraries.
- sudo make install installs OpenROAD system-wide (in /usr/local/bin), allowing it to be accessed from any directory in the terminal.
This stage transforms the source code into an executable EDA tool.

## Verify Installation 
```
ls OpenROAD/
ls OpenROAD/test/
```
- ls OpenROAD/ and ls OpenROAD/test/ check if the installation created the expected directory structure and test files.
- The command
  ```
  openroad -gui -log gcd_logfile.log gcd_sky130hs.tcl
  ```

![WhatsApp Image 2025-11-03 at 11 45 49 AM](https://github.com/user-attachments/assets/3dc5762e-ab64-45cf-9a76-2ac2f50bf51b)

launches OpenROAD in GUI mode and executes a test script.
-gui opens the graphical user interface for layout visualization.
-log stores the output in a log file for debugging and verification.
If the GUI opens successfully and the test runs without error, the installation is verified.

![WhatsApp Image 2025-11-03 at 11 45 50 AM](https://github.com/user-attachments/assets/7366adda-8d3b-42d6-bb4f-e88861b373e7)

## ⚠️ Common Issues and Fixes – OpenROAD Installation

| **No.** | **Issue / Error Message** | **Cause** | **Fix / Solution** |
|:--:|:--|:--|:--|
| 1 | `YOSYS_EXE not found` or `openroad: command not found` | OpenROAD or Yosys not compiled properly or PATH not set | Rebuild using `make` and add to PATH:<br>`export PATH=$PWD/build/src:$PATH` |
| 2 | `CMake Error: missing package (spdlog, boost, eigen3...)` | Missing required dependencies | Reinstall dependencies:<br>`sudo ./etc/DependencyInstaller.sh -base`<br>`./etc/DependencyInstaller.sh -common -local` |
| 3 | `Permission denied while running make install` | System-wide installation requires root access | Use:<br>`sudo make install`<br>or install locally using:<br>`cmake -DCMAKE_INSTALL_PREFIX=$HOME/OpenROAD ..` |
| 4 | `Segmentation fault (core dumped)` when launching GUI | Missing GUI libraries or running without display support | Install Qt libraries:<br>`sudo apt install qtbase5-dev libx11-dev`<br>or run:<br>`openroad -no_gui` |
| 5 | `cc1plus: fatal error: Killed signal terminated program` | Insufficient memory during compilation | Reduce parallel jobs:<br>`make -j2`<br>or create swap space to increase memory |

## 🙏 Acknowledgment

I am sincerely grateful to [**Kunal Ghosh**](https://github.com/kunalg123) and the entire  **[VLSI System Design (VSD)](https://vsdiat.vlsisystemdesign.com/)** team for this incredible opportunity to participate in the RISC-V SoC Tapeout Program and contribute to this nationwide initiative.

---








