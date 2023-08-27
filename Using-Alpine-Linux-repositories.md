## Make a backup!

If you have any worthwhile data in your file system, you really should do a backup before any major operation on the file system!

Do this by going into Settings - Filesystems - Select the one labeled as "Mounted at /" - Export. Once it is compressed you can select a location and name for this export.

If something goes wrong, all you need to do is to go to Settings - Filesystems - import 
and select your exported FS

# About using apk

Previously it was always necessary to first do `apk update` in order to retrieve the latest indexes and then do `apk upgrade` to update anything installed if a newer version is available. 
Since a few years the update step is auto executed when you do upgrade, so it is no longer needed. But old habits die hard, so almost everywhere you see people suggesting both steps. Nothing bad happens if you do both, but you reduce the amount of typing by only doing what is actually needed. It also saves a noticeable amount of time to not have apk processing the indexes twice.

The extra task `apk fix` is normally not needed, but it makes sense to do it after any major package manipulating action, since it will notice any glitches in the previous processes, and in most cases is able to auto fix them, if there are remaining unresolved issues they will be listed.

# Using Alpine Linux repositories

## Disable auto update of repository files

To replace iSH's own repositories, first disable the automatic processing of the repositories file that happens by iSH. Since their repositories are date based, any time they release a new date instance, an automated task needs to be triggered to change the repositories file. So you will pretty soon revert to the previous state. To disable this, all you need to do is to remove the /ish file tree, you do that like this: 

```sh
rm /ish -rf
```

If this is not present, iSH will not try to touch the repo file.

## Use an official Alpine repository

The packages in Alpine Linux repositories are more updated than iSH's own repositories and have packages whose size > 512 MB as well. 

Before doing this, one crucial step you need to do is to first check what release your current file system is based on, type: 

```sh
cat /etc/apk/repositories
``` 

And look for the sequence somewhat like this: `v3.14-2023-08-15` 
the release number part in this string is v3.14

But in the future it will most likely be a higher release.

Next is to point to an Alpine repo, either the primary listed below, or any of its mirrors.

You can use this snippet to do the change, but you need to make sure the release number
is not below what is already used!

```sh
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/main > /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/community >> /etc/apk/repositories
```

In the case the above is not the installed release, either edit it inside iSH after pasting,
or lacking knowledge in how to edit linux config files, first paste it into an environment
where you are familiar with editing text files and correct the release number.
Then copy the new snippet before pasting it into iSH.

Then do 

```sh
apk upgrade && apk fix
```

# Upgrading your file system

The upgrade to new release procedure at `https://wiki.alpinelinux.org/wiki/Upgrading_Alpine` 
is overly complicated when it comes to iSH, since iSH is its own kernel. 
It can be entirely ignored.

## Latest is not always best in the iSH case

When upgrading, it is often tempting to go for the latest release. In the case of iSH a bit of
caution would be wise. I have used 3.18 since it came out and only experienced a vim startup
glitch, just a set of error messages every time I started and exited it, but once in it worked fine. 
That was resolved by ISH dev team fairly quickly. But I have several colleagues that 
still prefer to stay on 3.16, since their apps work fine there, but they see issues with them
in 3.18

A new release typically is based on a newer kernel, with that comes that the apps are compiled
for that kernel, and thus the higher the release number, the more likely the expected kernel will
be using features not yet implemented in iSH.

Its not black or white, like a certain release can not be used at all, its more of a
sliding scale. Where apps demanding a lot from the cpu, tend to be heavily optimized and are quick
to use new kernel features. Whilst most apps have not changed, and thus they will typically work 
the same as in previous releases, unless a library they depend on now uses non iSH-compatible
kernel features.

As new releases come out, some early adopters try it right away, they often find what apps that
previously worked in iSH now fail. If that is your game, go for it! And pretty please report 
if you find things that used to work now failing!

If your iSH focus is more that you run certain apps and want to ensure they still work, 
then checking the Discord or googling things like: `ish alpine v3.18 go`
Will indicate if your important apps have issues with a certain new release.

Regardless of your usage style, as long as you did that backup, you might as well try the latest 
and see if things still work for you. If not import the backup and upgrade to less bleeding edge
release.

Be aware that the way Alpine is setup, there is no downgrade path, so once you have committed to 
a new release there is no way back, except for a full reinstall.

## Select a new release

All you need to do is point to a new release and do a regular apk upgrade

Please be aware that you need to use one of the official Alpine repositories for this to work.
If you still use the initial iSH repository, you are recommended to first follow the procedure
listed above in [Use an official Alpine repository](#use-an-official-alpine-repository)

All you need to do to upgrade for example from 3.14 to 3.16 or 3.18 is to edit 
/etc/apk/repositories and change the numbers into the release you want. 

In case you are unfamiliar with how to edit the file, you can re-use the snippet from 
[Use an official Alpine repository](#use-an-official-alpine-repository) above, 
replacing the release number with the release you want to upgrade into before pasting.

## Do the upgrade!

type: `apk upgrade && apk fix`

You are recommended to reboot once this is completed.

# Notes:

- [index.txt](https://github.com/ish-app/ish/blob/master/deps/aports/community/x86/index.txt) currently points to v3.14. Once this file points to a newer version, the above commands can be updated to match.
- iSH has its own repositories so the app is entirely self-contained and iSH with `apk` can pass app review. The repositories are a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.
- As explained in /etc/apk/repositories, the Alpine Linux repositories will be replaced by iSH's repositories after an `apk update` command is run.
