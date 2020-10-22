# Installing `apk` on the App Store Version
Due to Apple's restrictions on the App Store, `apk` had to be removed from the rootfs on the App Store. Thankfully it is very simple to get it back installed.
1. Run `wget http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86/apk-tools-static-2.10.5-r1.apk`
2. Run `tar xf apk-tools-static-2.10.5-r1.apk sbin/apk.static`
3. Run `./sbin/apk.static add apk-tools` to install `apk`
4. Profit