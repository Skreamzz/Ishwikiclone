OpenRC is the mechanism Alpine Linux uses to manage system services.  It can be used to start, stop and check the status of services such as sshd and the apache web server.  It can also be used to specify which services to run when an Alpine system boots.

This tutorial will show you how to make it work. There is a list of services and their status in iSH at the end of this docuent.

Getting everything going is actually fairly simple. The first thing you will need to do is install openrc with 
```
apk add openrc
```

Now you need to restart iSH, in order for the right run level to be selected.  Exit the app and launch it again.

Now type

```rc-status ```

You should see something similar to the following...
```
localhost:~# rc-status
Runlevel: default
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
localhost:~#
```

### Oddities with iSH

Be aware that since iSH is a fairly limited systems, whenever services are manually started or stopped, there will often be warnings displayed, such as:

```
Service 'hwdrivers' needs non existent service 'dev'
Service 'machine-id' needs non existent service 'dev'
grep: /proc/filesystems: No such file or directory
```

These can generally be ignored, they are due to stuff not yet implemented in iSH. 
As long as the line mentioning the service modified ends with `[ OK ]`, 
nothing bad happened.

## Installing a sample service - sshd

Install sshd `apk add openssh`

To add it as a service `rc-update add sshd`

This has added the service, so it will be auto started on future bootups.

To remove the service, type `rc-update del sshd`

Same as with the add, this only takes effect on any future bootups.

To manually start it right away, not having to reboot for this to happen, type `rc-service sshd start`

If you haven't run sshd before, this will take a while, as the host keys are generated.
Once this slow first start has happened, future starts of sshd will be pretty instantaneous.

If you don't start it right away like above, it will still work, but the process will be much less obvious, since the fairly slow host key generation will happen behind the scenes during the next bootup.

Whenever in doubt if a service has started, like after a reboot you can type `rc-status`.  

As long as you don't see `[ failed ]` or `[ stopped ]` on the same line as a service, assume the startup hasn't completed yet. Give it a few moments and run `rc-status` again.
If you see `[ started ]` the service is running.

```
localhost:~# rc-status
Runlevel: default
 sshd                              [  started  ]
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
localhost:~#
```

To temporarily stop the service during the current iSH session, type `rc-service sshd stop`

Be aware that if the service is still active, it will auto start on next boot.

## Some services and their working status

Last update: 2023-08-27

### working

* sshd: Extensively tested
* dcron: Moderately tested
* apche2: Minimally tested
* nginx: Minimally tested

### Not working

* exim
* mysqld/mariadb
* syslog-ng - Starts but programs that attempt to log lock-up
* rsyslog - Starts but programs that attempt to log lock up
* dbus
* avahi-daemon

## Troubleshooting:

If you get something like:
```
:~# rc-status
-ash: rc-status: not found
```
Try:
```
apk add openrc
```