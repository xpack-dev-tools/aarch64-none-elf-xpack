---

title: The xPack GNU AArch64 Embedded GCC
permalink: /dev-tools/aarch64-none-elf-gcc/

summary: "A binary distribution of GNU AArch64 Embedded GCC."

keywords:
  - aarch64-none-elf-gcc
  - arm
  - gcc
  - embedded

comments: true

date: 2019-07-10 17:53:00 +0300

redirect_to: https://xpack-dev-tools.github.io/aarch64-none-elf-gcc-xpack/

---

## Quicklinks

If you already know the general facts about the xPack GNU AArch64 Embedded GCC, you can
directly skip to the desired pages.

User pages:

- [install]({{ site.baseurl }}/aarch64-none-elf-gcc/install/)
- [support]({{ site.baseurl }}/aarch64-none-elf-gcc/support/)
- [releases]({{ site.baseurl }}/aarch64-none-elf-gcc/releases/)

Developer & maintainer pages:

- [GitHub](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/)
- [README-MAINTAINER](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/blob/xpack/README-MAINTAINER.md)

## Overview

The **xPack GNU AArch64 Embedded GCC**
is an alternate binary distribution that complements the official
[GNU AArch64 Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm)
maintained by Arm.

## Benefits

The main advantages of using the **xPack GNU AArch64 Embedded GCC** are:

- a convenient, uniform and portable install/uninstall/upgrade procedure,
  the same procedure is used for all major
  platforms (Intel Windows 64-bit, Intel GNU/Linux 64-bit, Arm GNU/Linux
  64/32-bit, Intel macOS 64-bit, Apple Silicon macOS 64-bit)
- a convenient integration with Continuous Integration environments,
  like GitHub Actions
- a better integration with development environments
  like **Eclipse Embedded CDT**.

All binaries are self-contained, they include all required libraries,
and can be installed in any location.

## Compatibility

The **xPack GNU AArch64 Embedded GCC** is fully compatible with the
original GNU AArch64 Embedded Toolchain distribution by Arm.

Occasionally, when bugs are discovered and the yearly Arm release schedule
would add unacceptably long delays, the **xPack GNU AArch64 Embedded GCC**
moves ahead of Arm and uses more recent tools versions that fix the bugs.

## Install

The details of installing the **xPack GNU AArch64 Embedded GCC** on various
platforms are presented in the separate
[install]({{ site.baseurl }}/aarch64-none-elf-gcc/install/) page.

## Documentation

The original GNU GCC documentation is available
[online](https://gcc.gnu.org/onlinedocs/).

## Support

For the various support options, please read the separate
[support]({{ site.baseurl }}/aarch64-none-elf-gcc/support/) page.

## Change log

The release and change log is available in the repository
[`CHANGELOG.md`](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/blob/xpack/CHANGELOG.md) file.

## Build details

For those interested in building the binaries, please read the
[README-MAINTAINER](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/blob/xpack/README-MAINTAINER.md)
page.
However, the ultimate source for details are the build scripts themselves,
all available from the
[`aarch64-none-elf-gcc-xpack.git/scripts`](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/tree/xpack/scripts/)
folder.

## Releases

See the [releases]({{ site.baseurl }}/aarch64-none-elf-gcc/releases/) pages.
