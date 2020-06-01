To mount other file providers in iSH, you can simply run
```bash
mount -t ios <src> <dst>
```
where `<src>` will be ignored and `<dst>` is where to mount the file

Upon running the command like
```bash
mount -t ios . /mnt
```
a file picker will show up and you may select which folder to mount. 

Additionally, if jailbroken, you can also mount using real, absolute paths. To do so run:
```bash
mount -t real <src> <dst>
```
where `<src>` is the absolute path from the root of iOS and `<dst>` is the location in iSH to mount the file. 

To mount the whole iOS file system into iSH’s `/mnt` run:
```bash
mount -t real / /mnt
```