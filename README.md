# Python bindings for the nRF5 Bluetooth Low Energy GAP/GATT driver

## Introduction
pc-ble-driver-py is a serialization library over serial port that provides Python bindings
for the [pc-ble-driver  library](https://github.com/NordicSemiconductor/pc-ble-driver) library.

pc-ble-driver-py depends on the pc-ble-driver repository referrenced as a submodule.

These bindings include two different components:

* A shared library written in C that encapsulates the SoftDevice API and serializes it over UART.
* A set of Python files generated with SWIG that present the shared library API to Python applications.

# Compiling

Before building pc-ble-driver-py you will need to have Boost installed and some of its libraries statically compiled.
To install and compile Boost, please follow the instructions here:

[Installing and building Boost](https://github.com/NordicSemiconductor/pc-ble-driver/tree/self_contained_driver#installing-and-building-boost)

Assuming that you have built the Boost libraries and installed the tools required to do so, you can now build and install the Python bindings and the accompanying shared library.

**Note**: Make sure you have built the Boost libraries for the architecture (32 or 64-bit) required by your Python installation.

## Dependencies

To build this project you will need the following tools:

* [CMake](https://cmake.org/) (>=2.8.12)
* [SWIG](http://www.swig.org/)
* [Python](https://www.python.org/) (>= 2.7 && <= 3.0)
* A C/C++ toolchain (should already have been installed to build Boost)

See the following sections for platform-specific instructions on the installation of the dependencies.

### Windows 

* Install the latest CMake stable release by downloading the Windows Installer from:

[CMake Downloads](https://cmake.org/download/)

* Install the latest SWIG stable release by downloading the `swigwin-x.y.z` package from:

[SWIG Downloads](http://www.swig.org/download.html)

Then extract it into a folder of your choice. Append the SWIG folder to your PATH, for example if you have installed
SWIG in `c:\swig\swigwin-x.y.z`:

    PATH=%PATH%;c:\swig\swigwin-x.y.z;

* Install the latest Python 2 Release by downloading the installer from:

[Python Windows Downloads](https://www.python.org/downloads/windows/)

**Note**: Select the Python architecture (32 or 64-bit) that you plan to build for.

Install Microsoft Visual Studio. The following versions supported are:

* Visual Studio 2013 (MSVC 12.0)
* Visual Studio 2015 (MSVC 14.0)

Open a Microsoft Visual Studio Command Prompt and issue the following from the root folder of the repository:

    > cd build
    > cmake -G "Visual Studio XX <Win64>" <-DBOOST_LIBRARYDIR="<Boost libs path>>" ..
    > msbuild ALL_BUILD.vcxproj

**Note**: Select Visual Sutio 12 or 14 `-G "Visual Studio XX"` option.

**Note**: Add `Win64` to the `-G` option to build a 64-bit version of the driver.

**Note**: Optionally select the location of the Boost libraries with the `-DBOOST_LIBRARYDIR` option.

The results of the build will be placed in `build\outdir`.

#### Examples

Building for 32-bit Python with 64-bit Visual Studio 15:

    > cmake -G "Visual Studio 14" ..

Building for 64-bit Python with 64-bit Visual Studio 15 pointing to a 64-bit Boost build:

    > cmake -G "Visual Studio 14 Win64" -DBOOST_LIBRARYDIR="c:\boost\boost_1_61_0\stage\x64"..

### Ubuntu Linux

Install the required packages to build the bindings:

    $ sudo apt-get install cmake swig libudev-dev python python-dev

Then change to the root folder of the repository and issue the following commands:

    $ cd build
    > cmake -G "Unix Makefiles" <-DARCH=<x86_32,x86_64>> <-DBOOST_LIBRARYDIR="<Boost libs path>>" ..
    $ make

The results of the build will be placed in `build/outdir`.

**Note**: Optionally select the target architecture (32 or 64-bit) using the `-DARCH` option.

**Note**: Optionally select the location of the Boost libraries with the `-DBOOST_LIBRARYDIR` option.

### OS X 10.11 and later

Install cmake and swig with Homebrew with the `brew` command on a terminal:

    $ brew install cmake
    $ brew install swig

Then change to the root folder of the repository and issue the following commands:

    $ cd build
    $ cmake -G "Unix Makefiles" ..
    $ make

The results of the build will be placed in `build/outdir`.

