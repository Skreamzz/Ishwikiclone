iSH 1.1 includes the [APK package manager](https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management). To keep the app self contained while also not including gigabytes of packages, files are downloaded from the App Store as [on-demand resources](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/On_Demand_Resources_Guide).

If you updated from a previous version, you won't have the iSH-provided APK, since enabling it is a potentially destructive action (overwriting /etc/apk/repositories). To enable it manually, run this command after installing the 1.1 update:

```
mkdir -p /ish/apk && printf 'file:///ish/apk/main\nfile:///ish/apk/community\n' > /etc/apk/repositories && mount -t apk apk /ish/apk && tar -xf /ish/apk/main/x86/apk-tools-static-2.10.5-r1.apk -C / && apk.static add apk-tools && rm /sbin/apk.static && apk upgrade
```

If this fails with `mkdir: can't create directory '/ish/apk': Operation not permitted`, run this slightly different command:

```
printf 'file:///ish/apk/main\nfile:///ish/apk/community\n' > /etc/apk/repositories && tar -xf /ish/apk/main/x86/apk-tools-static-2.10.5-r1.apk -C / && apk.static add apk-tools && rm /sbin/apk.static && apk upgrade
```

Alternatively, if you have no important data, you may delete and reinstall the app to use the new default filesystem.

Starting from this build, the default iSH filesystem reserves the directory /ish for its own internal bookkeeping. A “default” filesystem is identified by the existence of a directory at /ish. The command above will create this directory. Current uses for this directory include updating the version file to match the build of iSH that it was opened with and mounting a synthetic filesystem to provide the ODRs necessary for the built-in APK. If you don't want this, run `umount /ish/apk && rm -rf /ish`.

If you run into any issues (which is not unlikely as we barely tested this), please contact us.

## Known issues

* We forgot to include the community repository in this version. We will fix this in the next update. Workaround: `echo 'file:///ish/apk/community' >> /etc/apk/repositories`
* If you already have a /ish directory, iSH will "take it over" by creating /ish/version. We realize this may cause problems for people who have created and are using /ish for other reasons. The next update will only reserve it for internal use if /ish/version exists. Workaround: `umount /ish/apk`, `rm /ish/version`, rename the directory.
* Resizing the terminal (e.g. hiding the keyboard, rotating the screen) will cancel any ongoing package downloads. We will fix this in the next update. Workaround: don't resize the terminal.
