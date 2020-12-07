The iSH App supports the ability to use filesystems other than the barebones Alpine Linux distribution it ships with.  Only one filesystem can be used at a time but many can be imported and used.

The Alpine Linux downloads page...

https://alpinelinux.org/downloads/

Is the easiest place to find an image to import.  Specifically you will want to choose the x86 "Mini Root Filesystem".  Download it with you iPad.  It will be saved in your iCloud Downloads folder.

Next open iSH and tap the screen.  You should see a gear icon near the lower right corner.  Tap on that.

Near the middle of the resulting popup window will be an option called "Filesystems".  Click on that.

You will now see a "Filesystems" popup.  Tap on "Import" in the upper right corner.

Now navigate to the Downloads folder and click on the Alpine mini root.  After a brief time you will be returned to the Filesystems window and the mini root will now appear as a choice.  Tap on it.

You will see several options including "Boot From This Filesystem".  Choose that.  iSH will appear to crash.  This is expected.  When you open it again you will have booted from the filesystem you imported and selected.

----

**Note:** Most filesystem don't work yet and it is because /bin/login or /sbin/init encountered a fatal error. In addition,some filesystem will never work in iSH because they don't have /sbin/init. Those filesystem needs to be patched.