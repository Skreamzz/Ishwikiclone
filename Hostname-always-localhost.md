Starting with iOS 17 Apple no longer supports the API that iSH uses to retrieve hostname from iOS. Until that is resolved this is a
workaround to handle this.

### Set hostname

Uppercase and dashes work, spaces cant be used

```shell
echo MyOwnIsh > /etc/hostname
```

### Alternate hostname cmd

```shell
#!/bin/sh
cat /etc/hostname
```

Save this as `/usr/local/bin/hostname` or to somewhere in your PATH before /bin where the
normal hostname cmd is located, I would suggest /usr/local/bin for such but you can use any location.

Then make it runable like this:

```shell
chmod 755 /path/to/alternate/hostname
```
This will show the intended hostname if you type hostname. If it doesn't check your PATH

```shell
echo $PATH
```

You want the directory where you saved your alternate hostname to be listed before /bin in your PATH, otherwise, it will not be found

### General tools, such as shell prompts etc

Adding an alternate hostname in /usr/local/bin will have close to no effect on system tools. They will typically not have /usr/local/bin in their PATH and in some cases, they are hardcoded to use /bin/hostname

For this reason, to get everything to use your intended hostname, you need to replace /bin/hostname with yours.

You can either soft link your alternate hostname to that location. That would be the best practice approach since then it is instantly obvious that something custom is being used, and if you change it you only need to do it in one place. But from a usability point of view it works just as well to copy your alternate hostname to that location.

```shell
rm /bin/hostname
ln -sf /usr/local/bin/hostname /bin/hostname
```

The thing to be aware of is that the next time /bin/hostname is updated by apk, your alternate will be replaced, so you will then need to repeat that step.

