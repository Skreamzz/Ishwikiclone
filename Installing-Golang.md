# Installing  Golang on ISH

This is a quick guide on how to Install a Golang ISH

1. Run `apk update`
2. Run `apk add --no-cache --virtual .build-deps bash gcc musl-dev openssl go `
3. Test to make sure Ruby is installed by typing `go version`, you should see something along the lines of 

```bash
go version go1.13.15 linux/386
```
