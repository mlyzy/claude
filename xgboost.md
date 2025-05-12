# XGBoost Installation and Testing Process

This document details the process of installing and testing XGBoost from source code.

## 1. Repository Clone

```bash
mkdir -p ~/xgboost_test && cd ~/xgboost_test
git clone --recursive https://github.com/dmlc/xgboost.git
cd xgboost
```

**Purpose**: Create a working directory and clone the XGBoost repository with all its submodules.
**Result**: Successfully cloned the main repository and its submodules (dmlc-core and gputreeshap).

## 2. System Dependencies Installation

```bash
sudo apt-get update
sudo apt-get install -y --fix-missing cmake build-essential python3-dev python3-pip
```

**Purpose**: Install necessary build tools and development packages.
**Components**:
- cmake: Build system generator
- build-essential: Contains essential build tools (gcc, g++, make)
- python3-dev: Python development headers
- python3-pip: Python package installer

**Result**: Successfully installed the required system dependencies.

## 3. Building XGBoost

```bash
cd ~/xgboost_test/xgboost
mkdir build
cd build
cmake ..
make -j4
```

**Purpose**: Configure and build XGBoost from source
**Steps**:
1. Create build directory
2. Configure build with CMake
3. Compile using make with 4 parallel jobs

**Result**: Successfully built XGBoost core library

## 4. Python Package Installation

```bash
cd ~/xgboost_test/xgboost/python-package
pip3 install -e .
```

**Purpose**: Install XGBoost Python package in editable mode
**Dependencies Installed**:
- numpy
- scipy
- nvidia-nccl-cu12 (for GPU support)

**Result**: Successfully installed XGBoost Python package

## 5. Installation Verification

```bash
python3 -c "import xgboost as xgb; print(xgb.__version__)"
```

**Purpose**: Verify that XGBoost is properly installed and can be imported
**Result**: Successfully imported XGBoost and confirmed version 3.1.0-dev is installed

## Summary

The installation process was completed successfully, resulting in a working XGBoost installation from source. The build process included both the core C++ library and the Python package. The installation was verified by successfully importing the package in Python and checking its version.

## Notes

- The installation was performed on an Ubuntu system
- The build includes both CPU and GPU support
- The installation was done in development mode (-e flag) which is useful for development and testing
- Some initial package installation attempts encountered temporary repository issues, but were resolved using --fix-missing flag
