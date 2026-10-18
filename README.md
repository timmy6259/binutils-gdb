# GNU binutils-gdb

This repository contains the source codes and modifications for the `mips64-elf-ld` package targeting rootless iOS.

## Modifications
only modifications are this README.md.

## Building (mips64-elf-ld)

You will need a rootless jailbroken iOS environment, with the following dependencies installed via a package manager like Sileo:

* `autoconf`
* `bison`
* `clang`
* `flex`
* `git`
* `libgmp10`
* `libgmp-dev`
* `libmpfr6`
* `libmpfr-dev`
* `llvm`
* `make`
* `texinfo`

### Compilation Steps

```bash
git clone https://github.com/timmy6259/binutils-gdb/

mkdir -p build-mips64
cd build-mips64

../configure \
  --disable-gas \
  --disable-binutils \
  --disable-gprof \
  --disable-shared \
  --disable-nls \
  --disable-werror \
  --target=mips64-elf \
  --prefix=/var/jb/usr/local \
  MAKEINFO=true \
  SHELL=/var/jb/usr/bin/sh \
  AR=llvm-ar

export CFLAGS="-DYY_CURRENT_BUFFER=YY_CURRENT_BUFFER_LVALUE -DYYLDLEX_CHAR=char -Wno-error=macro-redefined"

make all-ld SHELL=/var/jb/usr/bin/sh MAKEINFO=true -j\$(nproc)

make install SHELL=/var/jb/usr/bin/sh
```

## License
This project is licensed under the GNU General Public License v3 (GPLv3).
