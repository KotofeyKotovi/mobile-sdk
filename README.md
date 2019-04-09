# CARTO Mobile SDK 

CARTO Mobile SDK is a multi-platform mobile
mapping SDK written mostly in C++11 with bindings to numerous languages
(Java/C# for Android, ObjectiveC/C# for iOS and C# for Windows Phone).

This project contains the core part of the SDK, for samples, look at
the ['Usage' section](#usage).

# Building
**We strongly suggest to use the precompiled SDK versions that can be found in
the samples below (in ['Usage' section](#usage)).** The precompiled libraries include 
support for CARTO online services (basemaps, offline map packages, routing, etc).
Also, getting all the SDK dependencies resolved and waiting for the build
to complete can be very time-consuming.

## Dependencies
Use `git submodule` to resolve all source-level dependencies

```
git submodule update --init --remote --recursive
```

Special **swig** version (swig-2.0.11-nutiteq branch) is needed for generating language-specific wrappers, this can be downloaded from https://github.com/CartoDB/swig. Clone it and compile it using usual `./autogen.sh; ./configure; make` routine. Make sure build script refers to this one.

**Python 2.7.x** is used for build scripts

**CMake 3.14 or later** is required by build scripts

Android build requires **Android SDK** and **Android NDK r17** or later.

iOS build requires **XCode 7.3** or later.

Windows Phone build requires **Visual Studio 2017**.

## Building process
Be patient - full build will take 1+ hours. You can speed it up by limiting architectures and platforms where it is built.

Set up boost library:

```
cd libs-external/boost
./bootstrap.sh
./b2 headers
cd ../..
```

Go to 'scripts' library where the actual build scripts are located:

```
cd mobile-sdk/scripts
```

## Android build 
```
python swigpp-java.py --profile standard
python build-android.py --profile standard
```

## iOS build:
```
python swigpp-objc.py --profile standard
python build-ios.py --profile standard
```

## Xamarin Android build:
```
python swigpp-csharp.py --profile standard android
python build-xamarin.py --profile standard android
```

## Xamarin iOS build:
```
python swigpp-csharp.py --profile standard ios
python build-xamarin.py --profile standard ios
```

## Windows Phone build
```
python swigpp-csharp.py --profile standard winphone
python build-winphone.py --profile standard
```

## GDAL build for Android
Use precompiled GDAL library containing headers and .so files. Make symbolic links
from GDAL_precompiled/android to prebuilt/gdal and GDAL_precompiled/android to libs-external/gdal.

```
python swigpp-java.py --profile gisextensions
python build-android.py --profile gisextensions --android-abi=armeabi-v7a --android-abi=arm64-v8a --android-abi=x86
```

Note: you need to copy libgdal.so files from the GDAL_precompiled folder

# Usage
* Developer docs: https://carto.com/docs/carto-engine/mobile-sdk/
* Android sample app: https://github.com/CartoDB/mobile-android-samples
* iOS sample app: https://github.com/CartoDB/mobile-ios-samples
* .NET (Xamarin and Windows 10) sample app: https://github.com/CartoDB/mobile-dotnet-samples

# Support, Questions?
* Post to CARTO developer group: https://groups.google.com/forum/#!forum/cartodb
* Post an issue to this project, submit a Pull Request
* Commercial support options: sales@carto.com
