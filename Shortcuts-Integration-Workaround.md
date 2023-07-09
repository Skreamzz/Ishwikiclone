While iSH doesn't have direct integration with Apple's Shortcuts, you can get very close using a few tools.

1. The Files app integration so that Shortcuts can write files into the iSH file system. https://github.com/ish-app/ish/wiki/View-iSH-files-in-Files-App
2. The instructions for running an SSH server. https://github.com/ish-app/ish/wiki/Running-an-SSH-server
3. Create a `~/.profile` file that launches the SSH server.
4. Create a Shortcut that puts together the following steps.
   1. The Scripting "Open App" step to launch iSH.
   2. The Scripting "Wait" step to give the SSH server enough time to start.
   3. The Scripting "Run Script Over SSH" step to execute code in the iSH instance.
   4. A step to switch away from the iSH app. (Since iSH is no longer in front, the SSH server stops.

Also, if you want an iSH service to continue running the background, you can use location tracking to get iSH to continue running. https://github.com/ish-app/ish/wiki/Running-in-background

Create a script with the name `~/.ish-background` with the following contents and then launch the script using `. ~/.ish-background` using the Scripting "Run Script Over SSH".  When you are doing using the background process, you can just delete the file and wait a minute for the location tracking to time out.

```bash
# Launch a command to track the GPS location
cat /dev/location > /dev/null &
# Save the Process ID so you can kill it later
export BACKGROUND_PID=$!
# Use ( ... ) & to start a subshell in the background
(
  # For the numbers 1 to 60, repeat checking for the current file
  for i in $(seq 1 60); do
    # If the file still exists
    if [[ -f ~/.ish-background ]]; then
      # Then wait for the next minute.
      sleep 60
    fi
  done
  # After one hour (60 minutes/hour * 60 seconds/minute),
  # or after the file stop existing. Then kill the process,
  # that is checking for location.
  kill $BACKGROUND_PID
) &
```