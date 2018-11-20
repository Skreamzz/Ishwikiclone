You'll need a few things to build the project:
```
- Python 3
- Ninja
- Yarn (only when building for iOS)
- Meson (pip install meson)
- Clang and LLD (brew install llvm)
```

To set up your environment, `cd` to the project and run `meson build` to create a build directory in build. Then `cd` to the build directory and run `ninja`.

To set up a self-contained Alpine linux filesystem, download the Alpine minirootfs tarball for i386 from the [Alpine website](https://alpinelinux.org/downloads/) and run the `tools/fakefsify.py` script. Specify the minirootfs tarball as the first argument and the name of the output directory as the second argument. Then you can run things inside the Alpine filesystem with `./ish -f alpine /bin/login`, assuming the output directory is called alpine.

To compile the iOS app, just open the Xcode project and click run. There are scripts that should download and set up the alpine filesystem and create build directories for cross compilation and so on automatically.