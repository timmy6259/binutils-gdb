# GNU binutils-gdb

This repository contains the source codes and modifications for the `mips64-elf-ld` package targeting rootless iOS.

## Building (mips64-elf-ld)

You will need a rootless jailbroken iOS environment, with the following dependencies installed via a package manager like Sileo:

* `git`
* `autoconf`
* `clang`
* `make`
* `llvm`
* `bison`
* `flex`
* `texinfo`

### Compilation Steps

```bash
mkdir -p build-mips64
cd build-mips64

../binutils-gdb/configure \
  --disable-gas \
  --disable-binutils \
  --disable-gprof \
  --disable-shared \
  --disable-nls \
  --disable-werror \
  --target=mips64-elf \
  --prefix=/var/jb/usr/local \
  MAKEINFO=true \
  SHELL=/var/usr/bin/sh \
  AR=llvm-ar

export CFLAGS="-DYY_CURRENT_BUFFER=YY_CURRENT_BUFFER_LVALUE -DYYLDLEX_CHAR=char -Wno-error=macro-redefined"

make all-ld SHELL=/var/usr/bin/sh MAKEINFO=true -j\$(nproc)

make install SHELL=/var/usr/bin/sh
```

## License
This project is licensed under the GNU General Public License v3 (GPLv3).
