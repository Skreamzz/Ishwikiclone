Your first step before modifying the repository should be to consider creating a [backup](Making-a-backup) in case anything goes wrong.

In the code snippets in this document, it is assumed that you are the root user.

# Disabling Auto Update of Repository File

To replace iSH's own repositories, it's essential to first disable the automatic processing of the repositories file by iSH. Their repositories are date-based, and whenever a new date instance is released, an automated task triggers a replacement of the /etc/apk/repositories file, pointing to the new iSH apk.ish.app files, overwriting any changes pointing to other Alpine repositories. The reason for this is to make the iSH app conformant to AppStore policies, and should not be seen as a hostile action. Especially given the fact that an easy method of disabling this is provided.

To prevent this, you simply need to remove the `/ish` file tree like this:

```sh
rm /ish -rf
```

This folder only contains some files, indicating what version of the iSH apk index is currently used, helping the app to know when to replace /etc/apk/repositories. If this folder is not present, iSH won't attempt to modify the repo file. 

# Using an Official Alpine Repository

The packages in Alpine Linux repositories are more up-to-date than those in iSH's repositories and include packages with sizes greater than 512 MB.

Before proceeding, an important step is to check the release your current file system is based on. You can do this by typing:

```sh
cat /etc/apk/repositories
```

Look for a sequence resembling this: `v3.14-2023-08-15`. The release number in this string is `v3.14`. However, it might be a higher release in the future.

Next, you should point to an Alpine repo, either the primary one listed below or one of its mirrors. You can use this snippet to make the change:

```sh
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/main > /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/community >> /etc/apk/repositories
```

If your system is not currently using the 3.14 release, either edit `/etc/apk/repositories` inside iSH after pasting, or if you're not familiar with editing Linux config files, first paste this into an environment where you're comfortable editing text files and correct the release number. Then copy the updated snippet before pasting it into iSH.

After making this change, execute:

```sh
apk upgrade && apk fix
```

Since you have not changed the Alpine release, this procedure doesn't constitute a full system upgrade; you've simply adjusted the source from which you retrieve information about current package availability. Consequently, there's no need to reboot once this process has completed.

# Notes:

- [index.txt](https://github.com/ish-app/ish/blob/master/deps/aports/community/x86/index.txt) currently points to v3.14. Once this file points to a newer version, the above commands can be updated to match.
- iSH has its own repositories so the app is entirely self-contained and iSH with `apk` can pass app review. The repositories are a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.
- As explained in /etc/apk/repositories, the Alpine Linux repositories will be replaced by iSH's repositories after an `apk update` command is run.
