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

You can soft link the regular /bin/hostname with this

```shell
rm /bin/hostname
ln -sf /usr/local/bin/hostname /bin/hostname
```

The thing to be aware of is that next time /bin/hostname is updated by apk, your alternate will be replaced, so you would then need to repeat thatt step.

The advantage by doing this is that there is no risk any script not having /usr/local/bin
in PATH will end up displaying "localhost" instead of the intended hostname.
One such example is shell prompts.
