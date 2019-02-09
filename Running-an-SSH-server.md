Here's a quick step by step guide for running an ssh server.

1. `apk add openssh`
2. `ssh-keygen -A`
3. `passwd`
4. type a password
5. edit `/etc/ssh/sshd_config` and set `PermitRootLogin` to `yes`
6. `/usr/sbin/sshd`

You should now be able to ssh to your device with username root and the password you typed.