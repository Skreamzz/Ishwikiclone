# Using Alpine Linux repositories
The packages in Alpine Linux repositories are more updated the iSH's own repositories. To use it to replace iSH's own repositories, run:

 ```sh
grep -v "file:///ish/apk/" /etc/apk/repositories | dd of=/etc/apk/repositories bs=4194304
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/main >> /etc/apk/repositories
echo https://dl-cdn.alpinelinux.org/alpine/v3.12/community >> /etc/apk/repositories
```
