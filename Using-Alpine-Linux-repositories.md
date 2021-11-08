# Using Alpine Linux repositories

The packages in Alpine Linux repositories are more updated than iSH's own repositories and have packages whose size > 512 MB as well. To replace iSH's own repositories, run:
<!-- 3.13+ is not used due to missing seccomp(2) support -->
```sh
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/main >> /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.14/community >> /etc/apk/repositories
sed -i -e '/http:\/\/apk.ish.app/d' /etc/apk/repositories 
```

Notes:

- [index.txt](https://github.com/ish-app/ish/blob/master/deps/aports/community/x86/index.txt) currently points to v3.14. Once this file points to a newer version, the above commands can be updated to match.
- iSH has its own repositories so the app is entirely self-contained and iSH with `apk` can pass app review. The repositories are a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.
- As explained in /etc/apk/repositories, the Alpine Linux repositories will be replaced by iSH's repositories after an `apk update` command is run.
