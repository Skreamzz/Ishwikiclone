# Using Alpine Linux repositories
The packages in Alpine Linux repositories are more updated the iSH's own repositories and have packages whose size > 512 MB as well. To use it to replace iSH's own repositories, run:
<!-- Editor's note: 3.13+ is not used due to missing seccomp(2) support -->
 ```sh
grep -v "file:///ish/apk/" /etc/apk/repositories | dd of=/etc/apk/repositories bs=4194304
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/main >> /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/community >> /etc/apk/repositories
```

Note : The reason why iSH has it's own repositories is so that the app is entirely self-contained so that iSH with `apk` can pass app review. The repositories is a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.