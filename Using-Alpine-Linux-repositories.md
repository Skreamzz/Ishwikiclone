# Using Alpine Linux repositories
The packages in Alpine Linux repositories are more updated than iSH's own repositories and have packages whose size > 512 MB as well. To use it to replace iSH's own repositories, run:
<!-- 3.13+ is not used due to missing seccomp(2) support -->
 ```sh
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/main >> /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/community >> /etc/apk/repositories
sed -i -e '/http:\/\/apk.ish.app/d' /etc/apk/repositories 
```

Note : https://github.com/ish-app/ish/blob/master/deps/aports/community/x86/index.txt currently points to v3.12. Once this file points to a newer version, the above commands can be updated to match.

Note : The reason why iSH has its own repositories is so that the app is entirely self-contained so that iSH with `apk` can pass app review. The repositories are a pseudo `apk` filesystem mounted on /ish/apk that when read, will actually download from App Store as on-demand resources. It also means that Apple can review all packages in iSH's repositories.