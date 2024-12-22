---

title:  xPack GNU AArch64 Embedded GCC v11.2.1-1.1 released
sidebar: aarch64-none-elf-gcc

summary: "Version **11.2.1-1.1** is a new release; it follows the upstream Arm release."

arm_version: 11.2-2022.02
arm_date: February 15, 2022
version: 11.2.1-1.1
npm_subversion: 1
python_version: 10

download_url: https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/releases/tag/v11.2.1-1.1/

date: 2022-05-15 12:14:17 +0300

redirect_to: https://xpack-dev-tools.github.io/aarch64-none-elf-gcc-xpack/blog/2022/05/15/aarch64-none-elf-gcc-v11-2-1-1-1-released/

comments: true

categories:
  - releases
  - aarch64-none-elf-gcc

tags:
  - releases
  - arm
  - aarch64-none-elf-gcc
  - gcc
  - binaries
  - c++
  - exceptions

---

The [xPack GNU AArch64 Embedded GCC](https://xpack.github.io/dev-tools/aarch64-none-elf-gcc/)
is a standalone cross-platform binary distribution of
[GNU AArch64 Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain).

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
a dependency for a project is quite easy:

```sh
cd my-project
xpm init # Only at first use.

xpm install @xpack-dev-tools/aarch64-none-elf-gcc@latest

ls -l xpacks/.bin
```

To install this specific version, use:

```sh
xpm install @xpack-dev-tools/aarch64-none-elf-gcc@{{ page.version }}.{{ page.npm_subversion }}
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

To remove the links from the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/aarch64-none-elf-gcc
```

To completely remove the package from the central xPacks store:

```sh
xpm uninstall --global @xpack-dev-tools/aarch64-none-elf-gcc
```

## Compliance

The xPack GNU AArch64 Embedded GCC generally follows the official
[Arm Embedded GCC](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads/)
releases.

The current version is based on:

- [GNU AArch64 Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm)
release **{{ page.arm_version }}** from {{ page.arm_date }}
and uses the same sources. It includes:
  - GCC 11.2.1
  - binutils 2.37
  - newlib 4.1.0
  - GDB 11.2

## Supported libraries

The supported libraries are:

```console
$ aarch64-none-elf-gcc -print-multi-lib
.;
ilp32;@mabi=ilp32
```

## Changes

Compared to the official Arm version, there should be no functional changes.

### Python

Support for Python scripting was added to GDB. This distribution provides
a separate binary, `aarch64-none-elf-gdb-py3` with
support for **Python 3.{{ page.python_version }}**.

The Python 3 run-time is included, so GDB does not need any version of
Python to be installed, and is insensitive to the presence of other
versions.

### Text User Interface (TUI)

Support for TUI was added to GDB. The `ncurses` library (v6.3) was added to
the distribution.

{% include note.html content="TUI is not available on Windows." %}

## Bug fixes

- none

## Enhancements

- none

## Known problems

- for unknown reasons, in the Arm distribution used as reference,
  support for parsing XML files in GDB was disabled; when connecting
  to SEGGER J-Link GDB server, the warning _Can not parse XML target
  description; XML support was disabled at compile time_ is displayed
  and some functionality is not available; fixed in 11.2.1-1.2;
- due to an error in the build scripts, the libgcov.a library resulted
  with empty content; fixed in 11.2.1-1.2.

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

The original documentation is available
[online](https://gcc.gnu.org/onlinedocs/).

## Build

The binaries for all supported platforms
(Windows, macOS and GNU/Linux) were built using the
[xPack Build Box (XBB)](https://xpack.github.io/xbb/), a set
of build environments based on slightly older distributions, that should be
compatible with most recent systems.

The scripts used to build this distribution are in:

- `distro-info/scripts`

For the prerequisites and more details on the build procedure, please see the
[README-MAINTAINER](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/blob/xpack/README-MAINTAINER.md) page.

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
fdd941fa157fbd187a2168171a6222d53fbc02a1c21dc0454ce3b7315b3a3141
xpack-aarch64-none-elf-gcc-11.2.1-1.1-darwin-arm64.tar.gz

285e232032b71bc76cac796d3553072ad23c5efb928b8128bdb7bcb6d726852c
xpack-aarch64-none-elf-gcc-11.2.1-1.1-darwin-x64.tar.gz

83f2630bcc0fc04bacea477737dea76e2335e7380c38d4860d943bba46d6cef2
xpack-aarch64-none-elf-gcc-11.2.1-1.1-linux-arm.tar.gz

9e2753aea1d019f5c7853932b6b1afb623de11e4abe8ab367341a648d5b0e941
xpack-aarch64-none-elf-gcc-11.2.1-1.1-linux-arm64.tar.gz

f422b9a3a26c9801598233c9621d218c3c268547ed302d390061b2e9103bd188
xpack-aarch64-none-elf-gcc-11.2.1-1.1-linux-x64.tar.gz

e5c5bb40fc8820a45ebd359e61e82a98b6d0c136e24628b2cba668261a9d8683
xpack-aarch64-none-elf-gcc-11.2.1-1.1-win32-x64.zip

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
