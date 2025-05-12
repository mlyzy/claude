# OpenVPN Installation and Testing Process

This document summarizes the process of installing and testing OpenVPN from the source code.

## 1. Environment Preparation

### 1.1 Repository Cloning
```bash
mkdir -p /tmp/openvpn_test
cd /tmp/openvpn_test
git clone https://github.com/OpenVPN/openvpn.git
```

This creates a directory structure and clones the OpenVPN repository from GitHub.

### 1.2 Dependency Installation
```bash
sudo apt-get install -y autoconf automake libtool liblzo2-dev libssl-dev libpam0g-dev libnl-genl-3-dev libcap-ng-dev pkg-config
```

These commands install the essential dependencies required to build OpenVPN:
- autoconf, automake, libtool: Build system tools
- liblzo2-dev: Compression library
- libssl-dev: OpenSSL development files for encryption
- libpam0g-dev: PAM authentication support
- libnl-genl-3-dev: NetLink library for interfacing with kernel features
- libcap-ng-dev: Linux capabilities library

## 2. Building OpenVPN

### 2.1 Generating Build Configuration
```bash
cd /tmp/openvpn_test/openvpn
autoreconf -i -v -f
```

This command initializes the build system by:
- Creating the configure script
- Adding missing files
- Setting up automake and libtool

### 2.2 Configuring the Build
```bash
./configure --disable-lz4
```

The configure script:
- Determines system capabilities
- Verifies dependencies
- Creates Makefiles with appropriate settings
- We disabled LZ4 support (`--disable-lz4`) as the development package wasn't available

### 2.3 Compiling the Source
```bash
make -j$(nproc)
```

This command builds OpenVPN using all available CPU cores. The build process:
- Compiles the C source files
- Links libraries
- Creates the OpenVPN executable

## 3. Testing OpenVPN

### 3.1 Running the Test Suite
```bash
make check
```

The test suite results:
- 2 tests passed
- 3 tests skipped (no test configuration or environment available)
- 0 tests failed

### 3.2 Testing Crypto Functionality
```bash
src/openvpn/openvpn --genkey secret key
src/openvpn/openvpn --test-crypto --allow-deprecated-insecure-static-crypto --secret key
```

This test showed that:
- The basic crypto functionality works
- The BF-CBC cipher is not supported in the current OpenSSL version
- Static key functionality is deprecated and will be removed in OpenVPN 2.8

## 4. Observations and Notes

- OpenVPN 2.7 is moving away from static key encryption in favor of TLS-based security
- The build includes Linux-specific features like DCO (Data Channel Offload)
- Support for older ciphers like BF-CBC is being removed for security reasons
- The project uses a comprehensive test suite to verify functionality

## 5. Binary Details

The compiled OpenVPN binary:
```
File: /tmp/openvpn_test/openvpn/src/openvpn/openvpn
Size: 4.5MB
Features: SSL (OpenSSL), LZO, EPOLL, MH/PKTINFO, AEAD, DCO
```

## 6. Conclusion

OpenVPN was successfully built from source. The installation process involves several standard steps:
1. Installing dependencies
2. Configuring the build environment
3. Compiling the source code
4. Testing the functionality

The resulting binary is ready for deployment, but production use would typically involve creating proper configuration files and potentially integrating with system services.
