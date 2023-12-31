## Introduction

For the code snippets in this document, it is assumed that you are doing them as user root

OpenRC is the tool that Alpine Linux employs to manage services. It allows you to start, stop, and check the status of services such as `sshd` and the Apache web server. Additionally, you can use OpenRC to specify which services should run when an Alpine system boots.

This tutorial will guide you through the process. Towards the end of this document, you'll find a list of services and their status within iSH.

Getting everything up and running is relatively straightforward. The first step is to install OpenRC using the following command:

```sh
apk add openrc
```

Now, it's necessary to restart iSH to ensure the appropriate primary run level is selected. Exit the app and then relaunch it.

You will encounter an issue if you skip the reboot at this point. Because iSH booted up before OpenRC became available, OpenRC initially assumes the `sysinit` runlevel. Consequently, any services you add during this period are activated for the `sysinit` runlevel. This means those services start briefly as iSH initializes but are then terminated when iSH switches to the `default` runlevel.

Although this situation can be addressed through manual adjustments, performing a reboot at this stage entirely avoids this issue. After restarting iSH, it will operate in the correct `default` runlevel without any need for manual intervention.

Once you've completed the reboot, you can request a status update to obtain a list of active services and their statuses. At this point, no services will be running, but this step introduces you to the monitoring tool. Type the following command:

```sh
rc-status
```

You should see something similar to the following...

```sh
localhost:~# rc-status
Runlevel: default
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
localhost:~#
```

One crucial thing to check is that the current run level is set to `default`.
It should always be the case, if it is not, assign it this way:

```sh
openrc default
```

## Oddities with iSH

In a standalone Linux environment, system configuration occurs during startup, typically through init tasks. These tasks include actions like mounting file systems, initializing random numbers, and configuring networking.

However, in iSH, these system configuration tasks are handled by the iSH app before activating the virtual environment, and the virtual environment lacks access to hardware settings or network configuration.

Because of this lack of hardware access, such tasks will fail in iSH and display error messages. These errors, while harmless, can be a bit of an eyesore. The recommendation is to disable tasks related to system initiation and configuration when working in iSH.

In essence, in iSH, it's best to only start server daemons and background tasks via init scripts. Things like: sshd, apache, runbg

Keep in mind that iSH is a somewhat limited system, so when you manually start or stop services, you may encounter warnings like the following:

```sh
Service 'hwdrivers' needs non existent service 'dev'
Service 'machine-id' needs non existent service 'dev'
grep: /proc/filesystems: No such file or directory
```

These warnings can typically be ignored. They result from things not available in iSH. As long as the line mentioning the service status change ends with `[ OK ]`, there's no cause for concern.

## Installing a Sample Service - `sshd`

To install `sshd`, use the following command:

```sh
apk add openssh
```

To add `sshd` as a service that starts automatically on future boot-ups, 

```sh
rc-update add sshd
```

To remove the service from automatic startup, execute:

```sh
rc-update del sshd
```

Like the `add` command, this change will only affect future boot-ups.

If you want to manually start `sshd` immediately without rebooting, use this command:

```sh
rc-service sshd start
```

The initial start may take a bit longer as host keys are generated. Subsequent starts of `sshd` will be nearly instantaneous.

Even if you don't start it immediately as shown above, it will still work. However, the somewhat slow host key generation process will happen in the background during the next boot-up.

If you're uncertain whether a service has started, such as after a reboot, you can check its status by running:

```sh
rc-status
```  

As long as you don't see `[ failed ]` or `[ stopped ]` on the same line as a service, assume the startup hasn't completed yet. Give it a few moments and run `rc-status` again.
If you see `[ started ]` the service is running.

```sh
localhost:~# rc-status
Runlevel: default
 sshd                              [  started  ]
Dynamic Runlevel: hotplugged
Dynamic Runlevel: needed/wanted
Dynamic Runlevel: manual
localhost:~#
```

To temporarily stop a service during the current iSH session, use the following command:

```sh
rc-service sshd stop
```

Keep in mind that if the service is still active, it will automatically start during the next boot-up.

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
