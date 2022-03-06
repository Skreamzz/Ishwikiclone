iSH has a lot of issues running Go, and most programs won't compile. However, a fork ([iSH-AOK](https://github.com/emkey1/ish-AOK)) does support Go by enabling multicore (in later versions, disable the "Enable Multicore (Threading)" option in settings; in older versions, run `mc off` or edit `/proc/ish/defaults/enable_multicore` as root), albeit very slow.

1. Run `apk update`
2. Run `apk add go`
3. Test to make sure Go is installed by typing `go version`. You should see something along the lines of:

```bash
go version go1.13.15 linux/386
```
