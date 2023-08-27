# Using Alpine Linux repositories

Your first step before changing repository should be to consider making a [backup](Making-a-backup) in case something goes wrong.

## Disable auto update of repository files

To replace iSH's own repositories, first disable the automatic processing of the repositories file that happens by iSH. Since their repositories are date based, any time they release a new date instance, an automated task needs to be triggered to change the repositories file. So you will pretty soon revert to the previous state. To disable this, all you need to do is to remove the /ish file tree, you do that like this: 

```sh
sudo rm /ish -rf
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
sudo echo https://dl-cdn.alpinelinux.org/alpine/v3.14/main > /etc/apk/repositories
sudo echo https://dl-cdn.alpinelinux.org/alpine/v3.14/community >> /etc/apk/repositories
```

In the case the above is not the installed release, either edit it inside iSH after pasting,
or lacking knowledge in how to edit linux config files, first paste it into an environment
where you are familiar with editing text files and correct the release number.
Then copy the new snippet before pasting it into iSH.

Then do 

```sh
sudo apk upgrade && apk fix
```

# Notes:

- [index.txt](https://github.com/ish-app/ish/blob/master/deps/aports/community/x86/index.txt) currently points to v3.14. Once this file points to a newer version, the above commands can be updated to match.
- iSH has its own repositories so the app is entirely self-contained and iSH with `apk` can pass app review. The repositories are a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.
- As explained in /etc/apk/repositories, the Alpine Linux repositories will be replaced by iSH's repositories after an `apk update` command is run.
