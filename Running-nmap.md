nmap is a common an popular port scanning tool, used for checking for open/filtered/closed ports, both locally and externally.

On iSH, running `nmap <args> <ip/domain>` will produce an error:

![image](https://github.com/ish-app/ish/assets/34378390/e39fa36f-8021-4873-add2-a0cdb4dd1328)

To get past this, we can use the steps provided by [@HKTangyuan](https://github.com/HKTangyuan) from [this comment](https://github.com/ish-app/ish/issues/166#issuecomment-1454923663). These assume you've already installed `nmap`.

1. `adduser <user>`
2. `su <user>`
3. run `nmap <args> <ip/domain>`
*_<user> is to be replaced with your preferred subuser_

You'll still be confined by any functions that would require root privs, as well as you will have to run it as that user every single time. No Bueno!

There are additional steps that can be taken to make things a little easier.

First, lets add `sudo` and this new user to wheel:
1. `apk add sudo`
2. `echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel`
3. `adduser <user> wheel`

Second, lets install `runuser` via `apk add runuser`.

Last, we set an alias for nmap to use runuser to execute the command when still root
`alias nmap="runuser -u nmap -- nmap"`

Don't forget to make the alias permanent `echo "alias nmap=\"runuser -u nmap -- nmap\"" >> /etc/profile`

Depending on the args your use with nmap, you will still get some errors like this:

![image](https://github.com/ish-app/ish/assets/34378390/bd14c268-8a00-4a26-aba7-bd7068b7717e)


And this:

![image](https://github.com/ish-app/ish/assets/34378390/aa5af45d-d038-46d7-890d-99bc493eb3a5)

While it can be spammy and annoying, they do not seem to affect the BASIC functionality of nmap.

Copy Pasta:
```adduser nmap
apk add sudo
echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
adduser nmap wheel
apk add runuser
alias nmap="runuser -u nmap -- nmap"
echo "alias nmap=\"runuser -u nmap -- nmap\"" >> /etc/profile
nmap shiggl.es -sn
apk add nmap
nmap shiggl.es -sn```

