# OpenROAD Installation

## System Requirements

Before installing, make sure your system has:
OS: Ubuntu 20.04 / 22.04 (recommended)
RAM: ≥ 16 GB (32 GB preferred)
Disk: ≥ 50 GB free space
Tools: git, cmake, make, gcc/g++, python3

## Clone Repository
The first step, independent of the build method, is to download the repository:
```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD.git
cd OpenROAD
```

## Install Dependencies
```
sudo ./etc/DependencyInstaller.sh -base
./etc/DependencyInstaller.sh -common -local
```

## Build OpenROAD
```
mkdir build
cd build/
```

## Custom Library 
```
cmake ..
```

## System wide OpenROAD Install
```
make
sudo make install
```

## Verify Installation using test command
```
ls OpenROAD/
ls OpenROAD/test/
openroad -gui -log gcd_logfile.log gcd_nangate45_tcl








