The upgrade procedure detailed in [Alpine Linux's official documentation](https://wiki.alpinelinux.org/wiki/Upgrading_Alpine) can be overly complex when applied to iSH since iSH operates with its own kernel. Therefore, you can safely disregard that document for this process.

Before embarking on the upgrade, your first step should be to create a [backup](Making-a-backup) in case anything goes awry.

### Latest Isn't Always Greatest in the iSH Context

A new Alpine release typically builds upon a more recent kernel. As a result, the bundled apps are compiled to leverage the capabilities of this updated kernel. Consequently, as the release number increases, it becomes more likely that some apps may expect kernel features that haven't been implemented in iSH yet.

It's crucial to understand that this isn't a binary situation. It's more of a sliding scale. Apps that demand a lot from the CPU are often highly optimized and quick to adopt new kernel features. However, most apps remain unchanged, working just as they did in previous releases, unless they rely on a library that now uses non-iSH-compatible kernel features.

When new releases surface, early adopters often rush to give them a try. They may discover that apps which previously worked in iSH might now encounter issues. If you're one to embrace the cutting edge, feel free to dive right in. And, should you encounter apps that once worked but now fail, please report these issues. Your feedback is invaluable!

For those whose primary goal is to run specific apps and ensure their ongoing functionality, consider checking the Discord community or conducting online searches using terms like `ish alpine v3.18 go`. This will help you identify potential issues with critical apps when upgrading to a new release.

Regardless of your usage style, if you've been diligent in creating a backup, it's worthwhile to test the latest release to see if everything still functions as expected. If not, you can always restore from your backup and switch to a less cutting-edge release.

It's important to note that Alpine Linux doesn't offer a straightforward downgrade path. Once you commit to a new release, returning to the previous one isn't simple. Your options are limited to either performing a complete reinstallation or restoring from a backup created before the upgrade.

## Shutting Down Services

Shutting down all services offers the advantage of minimizing the risk of an older binary already running and accessing files that have been modified by a newer version of the same app. Although it's relatively rare, if such changes were to occur, they could potentially disrupt the data associated with that app.

If you haven't installed openrc, this step will fail, but it won't cause any harm. You'll simply receive a message stating `openrc: not found`. It's generally advisable to proceed with this step, with the only exception being if you're performing the upgrade via a remote session, as it would disconnect you.

To execute this step, type the following command:

```sh
sudo openrc shutdown
```

Despite the term "shutdown," nothing drastic will happen. This command instructs the init system to transition to the shutdown runlevel, which safely terminates all services. Your console session will remain active.

## Selecting a New Release

Please keep in mind that you need to use one of the official Alpine repositories for this to work correctly. If you're still using the initial iSH repository, it's recommended to first follow the procedure outlined in [Using Alpine Linux repositories](Using-Alpine-Linux-repositories).

To upgrade, for instance, from version 3.14 to 3.16 or 3.18, all you need to do is edit `/etc/apk/repositories` and replace the numbers with the release you desire.

If you're unsure about editing the file manually, you can use the snippet from [Using an official Alpine repository](Using-Alpine-Linux-repositories#use-an-official-alpine-repository), substituting the release number with the one you wish to upgrade to before pasting.

## Performing the Upgrade

To initiate the upgrade, use the following command:

```sh
sudo apk upgrade && sudo apk fix
```

Once this process is complete, it's essential to reboot your system.