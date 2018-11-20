## Setting up
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

## Further setup
To enable local development there are a few more steps that need to be done.
* Go to the project settings in Xcode find the `iSH` target.
* Under `General`, change the bundle identifier to a specific identifier for you.
* Under `Capabilities` change the name of the `App Group` and remove the old app group.
* Go to the "iSHFileProvider" target
* Under `General` use the same bundle identifier you created before and add `.FileProvider` to it.
* Under `Capabilities` use the same name of the `App Group` as for the `iSH` target.
* Go to the file `app/AppDelegate.m`.
* Change the string in the function manager `containerURLForSecurityApplicationGroupIdentifier:` to your App Group e that you entered in the step before.

**Congratulations!** You should now have the app running!