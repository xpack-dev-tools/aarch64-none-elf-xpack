---

title:  xPack GNU AArch64 Embedded GCC v12.3.1-2.1 released

summary: "Version **12.3.1-2.1** is a maintenance release; it fixes the GNU/Linux GDB issues with loading ELF files."

arm_version: "12.3.Rel1"
arm_date: "28 Jul, 2023"
gcc_version: "12.3.1"
binutils_version: "2.40"
gdb_version: "13.2"
newlib_version: "4.3.0"
python_version: "3.11.1"

version: "12.3.1-2.1"
npm_subversion: "1"

download_url: https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/releases/tag/v12.3.1-2.1/

comments: true

date: 2023-09-21 00:28:48 +0300

redirect_to: https://xpack-dev-tools.github.io/aarch64-none-elf-gcc-xpack/blog/2023/09/20/aarch64-none-elf-gcc-v12-3-1-2-1-released/

# For Jekyll releases selection.
categories:
  - releases
  - aarch64-none-elf-gcc

# For navigation; use scripts/createtag.sh in Jekyll.
tags:
  - releases
  - arm
  - aarch64-none-elf-gcc
  - gcc
  - binaries
  - c++
  - exceptions

---

The [xPack GNU AArch64 Embedded GCC](https://xpack.github.io/aarch64-none-elf-gcc/)
is a standalone cross-platform binary distribution of
[Arm GNU Toolchain](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain).

There are separate binaries for **Windows** (x64),
**macOS** (x64, arm64)
and **GNU/Linux** (x64, arm64 and arm).

{% include note.html content="The main targets for the GNU/Linux Arm
binaries are the **Raspberry Pi** class devices (armv7l and aarch64;
armv6 is not supported)." %}

## Download

The binary files are available from [GitHub Releases]({{ page.download_url }}).

## Prerequisites

- x64 GNU/Linux: any system with **GLIBC 2.27** or higher
  (like Ubuntu 18 or later, Debian 10 or later, RedHat 8 or later,
  Fedora 29 or later, etc)
- arm64/arm GNU/Linux: any system with **GLIBC 2.27** or higher
  (like Raspberry Pi OS, Ubuntu 18 or later, Debian 10 or later, RedHat 8 or later,
  Fedora 29 or later, etc)
- x64 Windows: Windows 7 with the Universal C Runtime
  ([UCRT](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)),
  Windows 8, Windows 10
- x64 macOS: 10.13 or later
- arm64 macOS: 11.6 or later

## Install

The full details of installing the **xPack GNU AArch64 Embedded GCC** on various platforms
are presented in the separate [Install]({{ site.baseurl }}/dev-tools/aarch64-none-elf-gcc/install/) page.

### Easy install

The easiest way to install Arm Embedded GCC is with
[`xpm`]({{ site.baseurl }}/xpm/)
by using the **binary xPack**, available as
[`@xpack-dev-tools/aarch64-none-elf-gcc`](https://www.npmjs.com/package/@xpack-dev-tools/aarch64-none-elf-gcc)
from the [`npmjs.com`](https://www.npmjs.com) registry.

With the `xpm` tool available, installing
the latest version of the package and adding it as
a development dependency for a project is quite easy:

```sh
cd my-project
xpm init # Add a package.json if not already present

xpm install @xpack-dev-tools/aarch64-none-elf-gcc@latest --verbose

ls -l xpacks/.bin
```

To install this specific version, use:

```sh
xpm install @xpack-dev-tools/aarch64-none-elf-gcc@{{ page.version }}.{{ page.npm_subversion }} --verbose
```

For xPacks aware tools, like the **Eclipse Embedded C/C++ plug-ins**,
it is also possible to install Arm Embedded GCC globally, in the user home folder.

```sh
xpm install --global @xpack-dev-tools/aarch64-none-elf-gcc@latest --verbose
```

Eclipse will automatically
identify binaries installed with
`xpm` and provide a convenient method to manage paths.

### Uninstall

To remove the links created by xpm in the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/aarch64-none-elf-gcc
```

To completely remove the package from the central xPack store:

```sh
xpm uninstall --global @xpack-dev-tools/aarch64-none-elf-gcc
```

## Compliance

The xPack GNU AArch64 Embedded GCC generally follows the official
[Arm GNU Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads/)
releases.

The current version is based on:

- [Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads/)
release **{{ page.arm_version }}** from {{ page.arm_date }}
and uses the same sources. It includes:
  - GCC {{ page.gcc_version }}
  - binutils {{ page.binutils_version }}
  - newlib {{ page.newlib_version }}
  - GDB {{ page.gdb_version }}

## Supported libraries

The supported libraries are:

```console
$ aarch64-none-elf-gcc -print-multi-lib
.;
ilp32;@mabi=ilp32
```

## Changes

Compared to the official Arm version, there should be no functional changes.

### XML parsing in GDB

Some advanced GDB servers, like the one provided with SEGGER J-Link, are
capable of passing an XML with the target capabilities to the GDB client.
For unknown reasons, the Arm toolchain distribution came without XML
parsing support. The xPack distribution brings back support for
XML parsing and full integration with the SEGGER J-Link GDB server.

### Python

Support for Python scripting was added to GDB. This distribution provides
a separate binary, `aarch64-none-elf-gdb-py3` with
support for **Python {{ page.python_version }}**.

The Python 3 run-time is included, so GDB does not need any version of
Python to be installed, and is insensitive to the presence of other
versions.

### Text User Interface (TUI)

Support for TUI was added to GDB. The `ncurses` library was added to
the distribution.

{% include note.html content="TUI is not available on Windows." %}

### No Guile

Due to the difficulties of building standalone Guile libraries on all
platforms, support for Guile scripting in GDB is currently not available.

## Bug fixes

- [[#2](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/issues/2)]
  due to a an issue in the build scripts, on GNU/Linux,
  the `aarch64-none-elf-gdb` was built without ELF support; fixed

## Enhancements

- none

## Known problems

- none

## Shared libraries

On all platforms the packages are standalone, and expect only the standard
runtime to be present on the host.

All dependencies that are build as shared libraries are copied locally
in the `libexec` folder (or in the same folder as the executable for Windows).

### `DT_RPATH` and `LD_LIBRARY_PATH`

On GNU/Linux the binaries are adjusted to use a relative path:

```console
$ readelf -d library.so | grep runpath
 0x000000000000001d (RPATH)            Library rpath: [$ORIGIN]
```

In the GNU ld.so search strategy, the `DT_RPATH` has
the highest priority, higher than `LD_LIBRARY_PATH`, so if this later one
is set in the environment, it should not interfere with the xPack binaries.

Please note that previous versions, up to mid-2020, used `DT_RUNPATH`, which
has a priority lower than `LD_LIBRARY_PATH`, and does not tolerate setting
it in the environment.

### `@rpath` and `@loader_path`

Similarly, on macOS, the binaries are adjusted with `install_name_tool` to use a
relative path.

## Documentation

The original GNU GCC documentation is available
[online](https://gcc.gnu.org/onlinedocs/).

## Build

The binaries for all supported platforms
(Windows, macOS and GNU/Linux) were built using the
[xPack Build Box (XBB)](https://xpack.github.io/xbb/), a set
of build environments based on slightly older distributions, that should be
compatible with most recent systems.

Ubuntu 18.04 LTS _Bionic Beaver_ reachedFor the prerequisites and more details on the build procedure, please see the
[How to build](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/blob/xpack/README-BUILD.md) page.

## CI tests

Before publishing, a set of simple tests were performed on an exhaustive
set of platforms. The results are available from:

- [GitHub Actions](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/actions/)
- [Travis CI](https://app.travis-ci.com/github/xpack-dev-tools/aarch64-none-elf-gcc-xpack/builds/)

## Tests

The binaries were tested on a variety of platforms,
but mainly to check the integrity of the
build, not the compiler functionality.

## Checksums

The SHA-256 hashes for the files are:

```txt
3bdae469f1479cf5535900aaf05c25b71f55cb17a0bbbea0eed41fc5e0371b31
xpack-aarch64-none-elf-gcc-12.3.1-2.1-darwin-arm64.tar.gz

4764aff79bdde32f44e91f3ecb3527ba1fb040669c513a0e6a29a990be7c3e41
xpack-aarch64-none-elf-gcc-12.3.1-2.1-darwin-x64.tar.gz

49c58c8c0ad0a44a0fc4c56136d56813922ce6f88eecaedb743b143a79082c5c
xpack-aarch64-none-elf-gcc-12.3.1-2.1-linux-arm.tar.gz

e3ae04e8489e38edacd7d3ff062747559016143fc476dc4e328e7db5c65f071e
xpack-aarch64-none-elf-gcc-12.3.1-2.1-linux-arm64.tar.gz

6063a0fd5b4bd1445bf0db1521839e2bb43daa2d3b974a2d9a8b8a76a8b9bcf3
xpack-aarch64-none-elf-gcc-12.3.1-2.1-linux-x64.tar.gz

41f87244a8c14a88d4926f20fee7e1087ba3ac7e128870a873e8bfa9e820ce92
xpack-aarch64-none-elf-gcc-12.3.1-2.1-win32-x64.zip

```

## Deprecation notices

### 32-bit support

Support for 32-bit x86 GNU/Linux and x86 Windows was
dropped in 2022. Support for 32-bit Arm GNU/Linux (armv7l) will be preserved
for a while, due to the large user base of 32-bit Raspberry Pi systems.

### GNU/Linux minimum requirements

Support for RedHat 7 was dropped in 2022 and the
minimum requirement was raised to GLIBC 2.27, available starting
with Ubuntu 18, Debian 10 and RedHat 8.

## Pre-deprecation notice for Ubuntu 18.04

Ubuntu 18.04 LTS _Bionic Beaver_ reached the end of the standard five-year
maintenance window for Long-Term Support (LTS) release on 31 May 2023.

As a courtesy, the xPack GNU/Linux releases will continue to be based on
Ubuntu 18.04 for another year.

From 2025 onwards, the GNU/Linux binaries will be built on **Debian 10**,
(**GLIBC 2.28**), and are also expected to run on RedHat 8.

Users are urged to update their build and test infrastructure to
ensure a smooth transition to the next xPack releases.

## Download analytics

- GitHub [xpack-dev-tools/aarch64-none-elf-gcc-xpack](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/)
  - this release [![Github All Releases](https://img.shields.io/github/downloads/xpack-dev-tools/aarch64-none-elf-gcc-xpack/v{{ page.version }}/total.svg)](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/releases/v{{ page.version }}/)
  - all xPack releases [![Github All Releases](https://img.shields.io/github/downloads/xpack-dev-tools/aarch64-none-elf-gcc-xpack/total.svg)](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/releases/)
  - [individual file counters](https://somsubhra.github.io/github-release-stats/?username=xpack-dev-tools&repository=aarch64-none-elf-gcc-xpack) (grouped per release)
- npmjs.com [@xpack-dev-tools/aarch64-none-elf-gcc](https://www.npmjs.com/package/@xpack-dev-tools/aarch64-none-elf-gcc)
  - latest releases [![npm](https://img.shields.io/npm/dw/@xpack-dev-tools/aarch64-none-elf-gcc.svg)](https://www.npmjs.com/package/@xpack-dev-tools/aarch64-none-elf-gcc/)
  - all @xpack-dev-tools releases [![npm](https://img.shields.io/npm/dt/@xpack-dev-tools/aarch64-none-elf-gcc.svg)](https://www.npmjs.com/package/@xpack-dev-tools/aarch64-none-elf-gcc/)

Credit to [Shields IO](https://shields.io) for the badges and to
[Somsubhra/github-release-stats](https://github.com/Somsubhra/github-release-stats)
for the individual file counters.
