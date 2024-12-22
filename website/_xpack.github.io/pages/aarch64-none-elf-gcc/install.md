---

title: How to install the xPack GNU AArch64 Embedded GCC binaries
permalink: /dev-tools/aarch64-none-elf-gcc/install/

summary: "The recommended method is via xpm."

version: "11.2.1"
xpack-subversion: "1.2"
version-timestamp: "20220111"

comments: true
toc: false

date: 2019-07-10 17:53:00 +0300

redirect_to: https://xpack-dev-tools.github.io/aarch64-none-elf-gcc-xpack/docs/install/

---

## Overview

The **xPack GNU AArch64 Embedded GCC** can be installed automatically,
via `xpm` (the
recommended method), or manually, by downloading and unpacking one of the
portable archives.

{% capture easy_install %}

## Easy install

The easiest way to install GNU AArch64 Embedded GCC is by using the
**binary xPack**, available as
[`@xpack-dev-tools/aarch64-none-elf-gcc`](https://www.npmjs.com/package/@xpack-dev-tools/aarch64-none-elf-gcc)
from the [`npmjs.com`](https://www.npmjs.com) registry.

### Prerequisites

The only requirement is a recent
`xpm`, which is a portable
[Node.js](https://nodejs.org) command line application. To install it,
follow the instructions from the
[xpm install]({{ site.baseurl }}/xpm/install/) page.

### Install

With xpm available, installing
the latest version of the package is quite easy:

```sh
cd my-project
xpm init # Only at first use.

xpm install @xpack-dev-tools/aarch64-none-elf-gcc@latest --verbose
```

This command will always install the latest available version,
in the global xPacks store, which is a platform dependent folder
(check the output of the `xpm` command for the actual folder used on
your platform).

{% capture include_1 %}
The install location can be configured using the
`XPACKS_STORE_FOLDER` environment variable; for more details please check the
[xpm folders]({{ site.baseurl }}/xpm/folders/) page.
{% endcapture %}

{% include tip.html content=include_1 %}

{% include tip.html content="The archive content is unpacked into a folder
named `.content`. On some platforms
this might be hidden for normal browsing, and require
separate options (like `ls -A`) or, in file browsers, to enable
settings like **Show Hidden Files**." %}

xPacks aware tools, like the **Eclipse Embedded CDT plug-ins** automatically
identify binaries installed with
xpm and provide a convenient method to manage paths.

{% include important.html content="Automatic
path discovery for the packages from the new `@xpack-dev-tools` scope was
added to **GNU MCU Eclipse plug-ins** with v6.3.x in 2022-07; update
older versions or configure the path manually." %}

### Update

For the moment, to update the package, try to install the latest release again,
as shown before. If there is a new release, it will be installed,
otherwise a message will warn that the package is already installed.

Future versions of xpm will implement the `outdated` and `update` commands,
as npm does.

### Uninstall

To remove the links from the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/aarch64-none-elf-gcc
```

To completely remove the package from the central xPacks store:

```sh
xpm uninstall --global @xpack-dev-tools/aarch64-none-elf-gcc --verbose
```

{% endcapture %}

{% capture manual_install %}

## Manual install

For all platforms, the **xPack GNU AArch64 Embedded GCC** binaries are
released as portable
archives that can be installed in any location.

The archives can be downloaded from the
GitHub [releases](https://github.com/xpack-dev-tools/aarch64-none-elf-gcc-xpack/releases/)
pages.
{% endcapture %}

{% capture windows %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```doscon
C:\>%USERPROFILE%\AppData\Roaming\xPacks\@xpack-dev-tool\aarch64-none-elf-gcc\{{ page.version }}-{{ page.xpack-subversion }}.1\.content\bin\aarch64-none-elf-gcc.exe" --version
aarch64-none-elf-gcc.exe (xPack GNU AArch64 Embedded GCC x86_64) {{ page.version }} {{ page.version-timestamp }}
```

{{ manual_install }}

### Download

The Windows versions of **xPack GNU AArch64 Embedded GCC**
are packed as ZIP files.
Download the latest version named like:

- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-win32-x64.zip`

{% include note.html content="In case you wonder where the suffix comes
from, it is exactly the Node.js `process.platform` and `process.arch`.
The `win32` part is confusing, but we have to live with it." %}

### Unpack

To manually install the xPack GNU AArch64 Embedded GCC,
unpack the archive and copy the versioned folder into the
`%USERPROFILE%\AppData\Roaming\xPacks\aarch64-none-elf-gcc`
(for example `C:\Users\ilg\AppData\Roaming\xPacks\aarch64-none-elf-gcc`) folder;
according to Microsoft, `AppData\Roaming` is the recommended location for
installing user specific packages.

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is slightly different from the xpm install folders,
which use the scope (like `@xpack-dev-tools`) to group different tools,
and `.content` to store the unpacked archive." %}

{% include important.html content="Although perfectly possible to
install GNU AArch64 Embedded GCC in any folder, it is highly recommended
to use this path, since by default the Eclipse Embedded CDT plug-ins search
for the executables in this location." %}

### Test

To check if the manually installed GCC starts, use something like:

```doscon
C:\>%USERPROFILE%\AppData\Roaming\xPacks\aarch64-none-elf-gcc\xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}\bin\aarch64-none-elf-gcc.exe" --version
aarch64-none-elf-gcc (xPack GNU AArch64 Embedded GCC x86_64) {{ page.version }} {{ page.version-timestamp }}
```

### Windows Build Tools

{% include tip.html content="Since Windows does not provide the GNU make
binaries, it is recommended to also install the **Windows Build Tools**." %}

{% endcapture %}

{% capture macos %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```console
$ ~/.local/xPacks/@xpack-dev-tools/aarch64-none-elf-gcc/{{ page.version }}-{{ page.xpack-subversion }}.1/.content/bin/aarch64-none-elf-gcc --version
aarch64-none-elf-gcc (xPack GNU AArch64 Embedded GCC x86_64) {{ page.version }} {{ page.version-timestamp }}
```

{{ manual_install }}

### Download

The macOS versions of **xPack GNU AArch64 Embedded GCC**
are packed as `.tar.gz` archives.
Download the latest version named like:

- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-x64.tar.gz`
- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-arm64.tar.gz`

### Unpack

To manually install the xPack GNU AArch64 Embedded GCC,
unpack the archive and copy it to
`~/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-<version>`:

```sh
mkdir -p ~/.local/xPacks/aarch64-none-elf-gcc
cd ~/.local/xPacks/aarch64-none-elf-gcc

tar xvf ~/Downloads/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-x64.tar.gz
chmod -R -w xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
```

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is different from the xpm install folders." %}

{% include important.html content="Although perfectly possible to
install GNU AArch64 Embedded GCC in any folder, it is highly recommended
to use this path, since by default the GNU MCU Eclipse plug-ins search
for the executables in this location." %}

The result is a structure like:

```console
$ tree -L 2 /Users/ilg/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
/Users/ilg/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
├── README.md
├── aarch64-none-elf
│   ├── bin
│   ├── include
│   ├── lib
│   └── share
├── bin
│   ├── aarch64-none-elf-addr2line
│   ├── aarch64-none-elf-ar
│   ├── aarch64-none-elf-as
│   ├── aarch64-none-elf-as-py3
│   ├── aarch64-none-elf-c++
│   ├── aarch64-none-elf-c++filt
│   ├── aarch64-none-elf-cpp
│   ├── aarch64-none-elf-elfedit
│   ├── aarch64-none-elf-g++
│   ├── aarch64-none-elf-gcc
│   ├── aarch64-none-elf-gcc-{{ page.version }}
│   ├── aarch64-none-elf-gcc-ar
│   ├── aarch64-none-elf-gcc-nm
│   ├── aarch64-none-elf-gcc-ranlib
│   ├── aarch64-none-elf-gcov
│   ├── aarch64-none-elf-gcov-dump
│   ├── aarch64-none-elf-gcov-tool
│   ├── aarch64-none-elf-gdb
│   ├── aarch64-none-elf-gdb-add-index
│   ├── aarch64-none-elf-gdb-add-index-py3
│   ├── aarch64-none-elf-gdb-py3
│   ├── aarch64-none-elf-gfortran
│   ├── aarch64-none-elf-gprof
│   ├── aarch64-none-elf-gprof-py3
│   ├── aarch64-none-elf-ld
│   ├── aarch64-none-elf-ld.bfd
│   ├── aarch64-none-elf-lto-dump
│   ├── aarch64-none-elf-nm
│   ├── aarch64-none-elf-objcopy
│   ├── aarch64-none-elf-objdump
│   ├── aarch64-none-elf-ranlib
│   ├── aarch64-none-elf-readelf
│   ├── aarch64-none-elf-size
│   ├── aarch64-none-elf-strings
│   └── aarch64-none-elf-strip
├── distro-info
│   ├── CHANGELOG.md
│   ├── licenses
│   ├── patches
│   └── scripts
├── include
│   └── gdb
├── lib
│   ├── bfd-plugins
│   ├── gcc
│   ├── libcc1.0.so
│   ├── libcc1.so -> libcc1.0.so
│   └── python3.10
├── libexec
│   ├── gcc
│   ├── libcrypt.2.dylib
│   ├── libcrypto.1.1.dylib
│   ├── libffi.8.dylib
│   ├── libgcc_s.1.dylib
│   ├── libgmp.10.dylib
│   ├── libiconv.2.dylib
│   ├── libisl.15.dylib
│   ├── liblzma.5.dylib
│   ├── libmpc.3.dylib
│   ├── libmpfr.4.dylib
│   ├── libncurses.6.dylib
│   ├── libpanel.6.dylib
│   ├── libpython3.10.dylib
│   ├── libreadline.8.1.dylib
│   ├── libreadline.8.dylib -> libreadline.8.1.dylib
│   ├── libsqlite3.0.dylib
│   ├── libssl.1.1.dylib
│   ├── libstdc++.6.dylib
│   ├── libz.1.2.12.dylib
│   └── libz.1.dylib -> libz.1.2.12.dylib
└── share
    ├── doc
    └── gcc-{{ page.version }}

21 directories, 59 files
```

### Test

To check if the manually installed GCC starts, use something like:

```console
$ ~/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}/bin/aarch64-none-elf-gcc --version
aarch64-none-elf-gcc (xPack GNU AArch64 Embedded GCC, 64-bit) {{ page.version }} 20191025 (release) [ARM/arm-9-branch revision 277599]
```

{% endcapture %}

{% capture linux %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```console
$ ~/.local/xPacks/@xpack-dev-tools/aarch64-none-elf-gcc/{{ page.version }}-{{ page.xpack-subversion }}.1/.content/bin/aarch64-none-elf-gcc --version
aarch64-none-elf-gcc (xPack GNU AArch64 Embedded GCC, 64-bit) {{ page.version }} 20191025 (release) [ARM/arm-9-branch revision 277599]
```

{{ manual_install }}

### Download

The GNU/Linux versions of **xPack GNU AArch64 Embedded GCC**
are packed as `.tar.gz` archives.
Download the latest version named like:

- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-x64.tar.gz`
- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-arm.tar.gz`
- `xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-arm64.tar.gz`

As the name implies, these are GNU/Linux `tar.gz` archives; they were build on
Ubuntu, but can be executed on most recent GNU/Linux distributions.

### Unpack

To manually install the xPack GNU AArch64 Embedded GCC,
unpack the archive and copy it to
`~/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-<version>`:

```sh
mkdir -p ~/.local/xPacks/aarch64-none-elf-gcc
cd ~/.local/xPacks/aarch64-none-elf-gcc

tar xvf ~/Downloads/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-x64.tar.gz
chmod -R -w xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
```

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is slightly different from the xpm install folders,
which use the scope (like `@xpack-dev-tools`) to group different tools,
and `.content` to store the unpacked archive." %}

{% include important.html content="Although perfectly possible to
install GNU AArch64 Embedded GCC in any folder, it is highly recommended
to use this path, since by default the Eclipse Embedded CDT plug-ins search
for the executables in this location." %}

The result is a structure like:

```console
$ tree -L 2 /home/ilg/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
/home/ilg/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}
├── aarch64-none-elf
│   ├── bin
│   ├── include
│   ├── lib
│   └── share
├── bin
│   ├── aarch64-none-elf-addr2line
│   ├── aarch64-none-elf-ar
│   ├── aarch64-none-elf-as
│   ├── aarch64-none-elf-as-py3
│   ├── aarch64-none-elf-c++
│   ├── aarch64-none-elf-c++filt
│   ├── aarch64-none-elf-cpp
│   ├── aarch64-none-elf-elfedit
│   ├── aarch64-none-elf-g++
│   ├── aarch64-none-elf-gcc
│   ├── aarch64-none-elf-gcc-{{ page.version }}
│   ├── aarch64-none-elf-gcc-ar
│   ├── aarch64-none-elf-gcc-nm
│   ├── aarch64-none-elf-gcc-ranlib
│   ├── aarch64-none-elf-gcov
│   ├── aarch64-none-elf-gcov-dump
│   ├── aarch64-none-elf-gcov-tool
│   ├── aarch64-none-elf-gdb
│   ├── aarch64-none-elf-gdb-add-index
│   ├── aarch64-none-elf-gdb-add-index-py3
│   ├── aarch64-none-elf-gdb-py3
│   ├── aarch64-none-elf-gfortran
│   ├── aarch64-none-elf-gprof
│   ├── aarch64-none-elf-gprof-py3
│   ├── aarch64-none-elf-ld
│   ├── aarch64-none-elf-ld.bfd
│   ├── aarch64-none-elf-lto-dump
│   ├── aarch64-none-elf-nm
│   ├── aarch64-none-elf-objcopy
│   ├── aarch64-none-elf-objdump
│   ├── aarch64-none-elf-ranlib
│   ├── aarch64-none-elf-readelf
│   ├── aarch64-none-elf-size
│   ├── aarch64-none-elf-strings
│   ├── aarch64-none-elf-strip
│   ├── libgpm.so.2 -> libgpm.so.2.1.0
│   └── libgpm.so.2.1.0
├── distro-info
│   ├── CHANGELOG.md
│   ├── licenses
│   ├── patches
│   └── scripts
├── include
│   └── gdb
├── lib
│   ├── bfd-plugins
│   ├── gcc
│   └── python3.10
├── lib64
│   ├── libcc1.so -> libcc1.so.0.0.0
│   ├── libcc1.so.0 -> libcc1.so.0.0.0
│   └── libcc1.so.0.0.0
├── libexec
│   ├── gcc
│   ├── libcrypto.so.1.1
│   ├── libcrypt.so.1 -> libcrypt.so.1.1.0
│   ├── libcrypt.so.1.1.0
│   ├── libexpat.so.1 -> libexpat.so.1.6.7
│   ├── libexpat.so.1.6.7
│   ├── libffi.so.8 -> libffi.so.8.1.0
│   ├── libffi.so.8.1.0
│   ├── libfl.so.2 -> libfl.so.2.0.0
│   ├── libfl.so.2.0.0
│   ├── libgcc_s.so.1
│   ├── libgmp.so.10 -> libgmp.so.10.4.1
│   ├── libgmp.so.10.4.1
│   ├── libiconv.so.2 -> libiconv.so.2.6.0
│   ├── libiconv.so.2.6.0
│   ├── libisl.so.15 -> libisl.so.15.0.0
│   ├── libisl.so.15.0.0
│   ├── liblzma.so.5 -> liblzma.so.5.2.5
│   ├── liblzma.so.5.2.5
│   ├── libmpc.so.3 -> libmpc.so.3.0.0
│   ├── libmpc.so.3.0.0
│   ├── libmpfr.so.4 -> libmpfr.so.4.1.6
│   ├── libmpfr.so.4.1.6
│   ├── libncurses.so.6 -> libncurses.so.6.3
│   ├── libncurses.so.6.3
│   ├── libpanel.so.6 -> libpanel.so.6.3
│   ├── libpanel.so.6.3
│   ├── libpython3.10.so.1.0
│   ├── libreadline.so.8 -> libreadline.so.8.1
│   ├── libreadline.so.8.1
│   ├── libsqlite3.so.0 -> libsqlite3.so.0.8.6
│   ├── libsqlite3.so.0.8.6
│   ├── libssl.so.1.1
│   ├── libstdc++.so.6 -> libstdc++.so.6.0.29
│   ├── libstdc++.so.6.0.29
│   ├── libz.so.1 -> libz.so.1.2.12
│   └── libz.so.1.2.12
├── README.md
└── share
    ├── doc
    └── gcc-{{ page.version }}

22 directories, 78 files
```

### Test

To check if the manually installed GCC starts, use something like:

```console
$ ~/.local/xPacks/aarch64-none-elf-gcc/xpack-aarch64-none-elf-gcc-{{ page.version }}-{{ page.xpack-subversion }}/bin/aarch64-none-elf-gcc --version
aarch64-none-elf-gcc (xPack GNU AArch64 Embedded GCC x86_64) {{ page.version }} {{ page.version-timestamp }}
```

{% endcapture %}

{% include platform-tabs.html %}

{% include warning.html content="**DO NOT** add the toolchain path to
the user or system path!" %}
