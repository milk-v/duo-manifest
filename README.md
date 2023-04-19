# Milk-V Duo

## Quick Start

### 1. Install dependencies
An ubuntu system, virtual machine or local host, **Ubuntu 20.04 LTS** is recommended.
```
$ sudo apt install dialog python3-dev make git bc gcc flex bison ninja-build libssl-dev \
      rsync pkg-config device-tree-compiler squashfs-tools parted dosfstools cpio
```

### 2. Install cmake
CMake 3.16.5 or higher is required.
```
$ wget -c https://cmake.org/files/v3.19/cmake-3.19.3-Linux-x86_64.tar.gz
$ tar -zxvf cmake-3.19.3-Linux-x86_64.tar.gz
$ sudo mv cmake-3.19.3-Linux-x86_64 /usr/bin/
$ echo 'export PATH="/usr/bin/cmake-3.19.3-Linux-x86_64/bin:$PATH"' >> ~/.bashrc
$ source ~/.bashrc
```
Or use pip install CMake.
```
$ sudo apt install python-is-python3 python3-pip
$ pip install cmake
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
$ mkdir duo && cd duo
$ repo init -u https://github.com/milk-v/duo-manifest.git -b main -m milk-v_duo_cv180xb_sdk.xml
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


### FAQs

1. Why is only one core shown?

   Linux runs on one core only, the SDK for the other core is not yet publicly available.

2. Why is only 32M RAM shown?

   Some of the memory is allocated to [ION](https://github.com/milk-v/cvitek-build/blob/main/boards/default/dts/cv180x/cv180x_default_memmap.dtsi#L15). You can change the [value](https://github.com/milk-v/cvitek-build/blob/main/boards/cv180x/cv1800b_sophpi_duo_sd/memmap.py#L43) and recompile the image.
