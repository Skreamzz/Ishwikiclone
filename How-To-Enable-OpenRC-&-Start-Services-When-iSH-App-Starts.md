OpenRC is the mechanism Alpine Linux uses to manage system services.  It can be used to start, stop and check the status of services such as sshd and the apache web server.  It can also be used to specify which services to run when and Alpine system boots.

Strictly speaking iSH doesn't boot and as of iSH 1.0.1 build 77 Open RC does not work correctly.  This tutorial will show you how to make it (mostly) work.  I'll include a list of services at the end that I've verified as working with iSH.

Getting everything going is actually fairly simple.

The first thing you will need to do is edit /etc/inittab.  You can use your favorite editor.  Many people seem to like nano, but emacs or vi are options as well.

The third line of the file should like as follows...
```
::sysinit:/sbin/openrc sysinit
```
Change it to
```
::sysinit:/sbin/openrc
```
In other words, delete 'sysinit'.

While you are there you might want to comment out the extra tty's a little further down in the file.  There is currently no way to access them and they take up a bit of extra memory when they run.  To do that you would insert a 

\# (hash) 

In front of all the lines that begin "tty" EXCEPT "tty1".  Commenting that one out would be a bad plan.

Now you need to restart iSH.  Exit the app and launch it again.

If you haven't already, install sshd via 

```apk add openssh```

Now type

```rc-status ```

You should see something similar to the following...
```
(14:11 ish /~)-> rc-status
Runlevel: default
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
 sshd                                                                                                                                                
(14:11 ish /~)-> 
```
Now type

```rc-update add sshd```

You should see something similar to the following...
```
(14:13 ish /~)-> rc-update add sshd
 * service sshd added to runlevel default
(14:13 ish /~)-> 
```
Finally type 

`rc-status`.  You should see something similar to the following...
```
(14:13 ish /~)-> rc-status
Runlevel: default
 sshd                                                                                                                                                [  started  ]
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
```
I've verified that the following service at least start and appear to work as of iSH 1.0.1 Build 77

sshd: Extensively tested
dcron: Moderately tested
apche2: Minimally tested
nginx: Minimally tested

In addition I've tested the following and they do not work as of this time.

exim
mysqld/mariadb
syslog-ng: Starts but programs that attempt to log lock-up
rsyslog: Starts but programs that attempt to log lock up

