# GNU binutils-gdb

This repository contains the source codes and modifications for the `binutils-mips64-elf_iphonos-arm64` package targeting rootless iOS.

## Modifications
only modifications are this README.md.

## Building (binutils without gdb)

You need a rootless jailbroken iOS environment, with the following dependencies installed via a package manager like Sileo:

* `autoconf`
* `bison`
* `clang`
* `flex`
* `git`
* `libfl2`
* `libfl-dev`
* `libgmp10`
* `libgmp-dev`
* `libmpfr6`
* `libmpfr-dev`
* `llvm`
* `make`
* `texinfo`

### Compilation Steps

You need to use the MAKEINFO=true instead of the Actual makeinfo, because the compatible issues.  

```bash
git clone https://github.com/timmy6259/binutils-gdb/

mkdir -p build-mips64
cd build-mips64

../configure \
  --disable-gas \
  --disable-nls \
  --disable-werror \
  --disable-gdb \
  --disable-libdecnumber \
  --disable-readline \
  --disable-sim \
  --target=mips64-elf \
  --prefix=/var/jb/usr \
  AR_FOR_TARGET=llvm-ar \
  RANLIB_FOR_TARGET=llvm-ranlib \
  SHELL=/var/jb/usr/bin/sh \
  MAKEINFO=true \
  AR=llvm-ar \
  AS=llvm-as

export CFLAGS="-DYY_CURRENT_BUFFER=YY_CURRENT_BUFFER_LVALUE -DYYLDLEX_CHAR=char -Wno-error=macro-redefined"

make all-gas all-ld all-binutils all-gprof all-gprofng all-libctf SHELL=/var/jb/usr/bin/sh MAKEINFO=true -j$(nproc)

make install SHELL=/var/jb/usr/bin/sh MAKEINFO=true

## License
This project is licensed under the GNU General Public License v3 (GPLv3).
