# Building libjpeg-turbo for iOS

## Requirements

- Xcode 10.0 or later. I use 10.2.1.
- [libjpeg-turbo](https://github.com/libjpeg-turbo/libjpeg-turbo) 1.*. I use 1.5.3, the build script cannot support version 2.0 or later.
- [Homebrew](https://brew.sh), install other libraries. Run `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`.
- [automake](https://formulae.brew.sh/formula/automake#default) 1.7 or later. Run `brew install automake`.
- [autoconf](https://formulae.brew.sh/formula/autoconf) 2.56 or later. It's automake configure script builder. 
- [libtool](https://formulae.brew.sh/formula/libtool#default) 1.4 or later. Run `brew install libtool`.
- [NASM](https://formulae.brew.sh/formula/nasm#default) (if building x86 or x86-64 SIMD extensions). Run `brew install nasm`.

## Usage

1. Run `$ [sudo] chmod +x build.sh` (if `./build.sh` command not found).
2. Run `$ ./build.sh`.
3. You will find library in output directory.

## FAQ

### Architectures

Create architectures i386, x86_64, armv7, armv7s and arm64 by default. 
You can change `ARCHS` property which architecture you want in `build.sh` line 20.

### Check SDK version

Support minimum for iOS is 8.0 by default. `MIN_OS_VERSION` property in `build.sh`(line 19).

```
Important

Check and set the SDK_VERSION available, otherwise cannot work.

eg: /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS12.2.sdk
SDK_VERSION=12.2
```

### Change libjpeg-turbo version

1. open `build.sh`, update `TARGET_VERSION`(line 9).
2. download libjpeg-turbo and copy to src directory.

```
Important

Cannot support libjpeg-turbo version 2.0 or later.
```

### How to check library architectures

You can use `lipo -info` or `file` command check architectures.

```
eg:

$ file libjpeg.a
 
libjpeg.a: Mach-O universal binary with 5 architectures: [i386:current ar archive random library] [arm64]
libjpeg.a (for architecture i386):	current ar archive random library
libjpeg.a (for architecture armv7):	current ar archive random library
libjpeg.a (for architecture armv7s):current ar archive random library
libjpeg.a (for architecture x86_64):current ar archive random library
libjpeg.a (for architecture arm64):	current ar archive random library

$ lipo -info libturbojpeg.a 

Architectures in the fat file: libturbojpeg.a are: i386 armv7 armv7s x86_64 arm64
```

### CVE

Submit libjpeg-turbo for [searching CVE list](https://cve.mitre.org/cve/search_cve_list.html).