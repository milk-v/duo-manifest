# Milk-V Duo

## Quick Start

### 1. Install dependencies
```
$ sudo apt install dialog python3-dev make git bc gcc flex bison ninja-build libssl-dev \
      rsync pkg-config device-tree-compiler squashfs-tools parted dosfstools
```

### 2. Install cmake
CMake 3.16.5 or higher is required.
```
$ wget -c https://cmake.org/files/v3.19/cmake-3.19.3-Linux-x86_64.tar.gz
$ tar -zxvf cmake-3.19.3-Linux-x86_64.tar.gz
$ sudo mv cmake-3.19.3-Linux-x86_64  /usr/bin
$ echo 'export PATH="/usr/bin/cmake-3.19.3-Linux-x86_64/bin:$PATH"'  >> ~/.bashrc
```

### 3. Download the repo
```
$ mkdir -p ~/.bin  
$ PATH="${HOME}/.bin:${PATH}"
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
$ chmod a+rx ~/.bin/repo
```

### 4. Get SDK source code
```
$ mkdir duo && duo
$ repo init -u git@github.com:milk-v/duo-manifest.git -b main -m milk-v_duo_cv180xb_sdk.xml
$ repo sync
```

### 5. Compile
```
$ source build/cvisetup.sh
$ defconfig cv1800b_sophpi_duo_sd
$ clean_all
$ build_all
$ pack_sd_image
```
The generated sd card image is located at **install/soc_cv1800b_sophpi_duo_sd/** and named sophpi-duo-\*.img

### 6. SD card burning
Use dd or [balenaEtcher](https://www.balena.io/etcher) to burn the image to the SD card.

```
$ cd install/soc_cv1800b_sophpi_duo_sd/
$ sudo dd if=./sophpi-duo-*.img of=/dev/sdx bs=32M status=progress oflag=direct
```

### 7. Boot

Insert the SD card and connect it to the power supply (5V). The board will boot the system from the SD card. The login password is **root** 