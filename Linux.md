You'll need a few things to build the project:
```
- Python 3
- Ninja
- Meson (pip install meson)
- Clang and LLD
```
You can get Clang and LLD by running `sudo apt install clang lld`, `sudo pacman -S clang lld` or whatever the equivalent is in your preferred package manager.

To set up your environment, `cd` to the project and run `meson build` to create a build directory in build. Then `cd` to the build directory and run `ninja`.

To set up a self-contained Alpine linux filesystem, download the Alpine minirootfs tarball for i386 from the [Alpine website](https://alpinelinux.org/downloads/) and run the `tools/fakefsify.py` script. Specify the minirootfs tarball as the first argument and the name of the output directory as the second argument. Then you can run things inside the Alpine filesystem with `./ish -f alpine /bin/login`, assuming the output directory is called alpine.

You can replace `ish` with `tools/ptraceomatic` to run the program in a real process and single step and compare the registers at each step. It can be used for debugging. Requires 64-bit Linux 4.11 or later.