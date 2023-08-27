The upgrade to new release procedure at `https://wiki.alpinelinux.org/wiki/Upgrading_Alpine` 
is overly complicated when it comes to iSH, since iSH is its own kernel. 
That document can be entirely ignored.

Your first step before upgrading to a new release should be to consider making a [backup](Making-a-backup) in case something goes wrong.

### Latest is not always best in the iSH case

When upgrading, it is often tempting to go for the latest release. In the case of iSH a bit of
caution would be wise. I have used 3.18 since it came out and only experienced a vim startup
glitch, just a set of error messages every time I started and exited it, but once in it worked fine. 
That was resolved by ISH dev team fairly quickly. But I have several colleagues that 
still prefer to stay on 3.16, since their apps work fine there, but they see issues with them
in 3.18

A new release typically is based on a newer kernel, with that comes that the apps are compiled
for that kernel, and thus the higher the release number, the more likely the expected kernel will
be using features not yet implemented in iSH.

Its not black or white, like a certain release can not be used at all, its more of a
sliding scale. Where apps demanding a lot from the cpu, tend to be heavily optimized and are quick
to use new kernel features. Whilst most apps have not changed, and thus they will typically work 
the same as in previous releases, unless a library they depend on now uses non iSH-compatible
kernel features.

As new releases come out, some early adopters try it right away, they often find what apps that
previously worked in iSH now fail. If that is your game, go for it! And pretty please report 
if you find things that used to work now failing!

If your iSH focus is more that you run certain apps and want to ensure they still work, 
then checking the Discord or googling things like: `ish alpine v3.18 go`
Will indicate if your important apps have issues with a certain new release.

Regardless of your usage style, as long as you did that backup, you might as well try the latest 
and see if things still work for you. If not import the backup and upgrade to a less bleeding edge
release.

Be aware that the way Alpine is setup, there is no downgrade path, so once you have committed to 
a new release there is no way back, except for a full reinstall.

## Select a new release

All you need to do is point to a new release and do a regular apk upgrade

Please be aware that you need to use one of the official Alpine repositories for this to work.
If you still use the initial iSH repository, you are recommended to first follow the procedure
listed in [Using Alpine Linux repositories](Using-Alpine-Linux-repositories)

All you need to do to upgrade for example from 3.14 to 3.16 or 3.18 is to edit 
/etc/apk/repositories and change the numbers into the release you want. 

In case you are unfamiliar with how to edit the file, you can re-use the snippet from 
[Use an official Alpine repository](Using-Alpine-Linux-repositories#use-an-official-alpine-repository), 
replacing the release number with the release you want to upgrade into before pasting.

## Shut down services

The advantage of shutting down all services is that you minimize the risk of an old binary already running,
accessing files also touched by a new version of the same app. Where the upgrade included some changes how files are written. This is pretty rare, but if it were to happen, it could cause utter mayhem with the data related to that app.

If you have not installed openrc, this step will fail but in a harmless way, you will just get a message
`openrc: not found`, you are better off doing this step. 
The only exception being if you are doing the upgrade via a remote session, this would disconnect you!

type: 

```sh
sudo openrc shutdown
```

Despite the word shutdown above, nothing drastic will happen. All this does is to tell the init system to 
enter the shutdown runlevel. This will terminate all services in a safe way. Your console session will continue


## Do the upgrade!

type: 

```sh
sudo apk upgrade && apk fix
```

Once this is completed you need to reboot.