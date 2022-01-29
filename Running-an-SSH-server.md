Here's a quick step by step guide for running an ssh server.

1. `$ apk add openssh` — install the ssh tools and the ssh server.
1. `$ ssh-keygen -A` — create the host keys.
1. `$ passwd` — Set a password for root to protect your iOS device
1. `$ echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config`
1. `$ /usr/sbin/sshd`

You should now be able to ssh to your device with username root and the password you typed.

### SSH from the same device

If you are trying to connect via ssh from the same device, make sure you set the port configuration of sshd to use a non standard one (greater than 1024, eg: 22000).

You can do this by editing `/etc/ssh/sshd_config` and set `Port 22000` (Replace _22000_ with any non-standard port).

After this, you can ssh (from iSH itself) using `ssh root@localhost -p 22000`

### Troubleshooting passwordless login

To login as root without a password, I follow the usual steps to create a key with ssh-keygen and ssh-copy-id the public key to the phone.  But upon login, I am still prompted for password.  Permission of .ssh dir is 700, and permission of authorized_keys is 600.

On the iPhone I stop the sshd server:

```
service sshd stop
```
 And restart in debug mode:
```
/usr/sbin/sshd -d -p 22
```

Now the ssh server on the phone is listening and will log activity to the screen.  I open another terminal window and ssh to the phone as root.  I am prompted for the password, but do not enter it yet.  Over in the debug output I see the following message:

`trying public key file /root/.ssh/authorized_keys`

`Authentication refused: bad ownership or modes for directory /root`

I enter the password, and am logged into the phone as root.  I change the ownership like this:

```
chown root /root
```
```
chown root /root/.ssh
```

And logout.  Now when I ssh to the phone as root, I am logged in successfully with the key, and not prompted for a password.

