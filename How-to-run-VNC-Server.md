Run `apk add alpine-baselayout alpine-keys  apk-tools busybox consolekit2 libc-utils lxdm sudo x11vnc xfce4 xfce4-terminal xorg-server xvfb xterm` to add all the required packages to run the VNC Server. 

Start backgrounding so we can connect with app not open`cat /dev/location > /dev/null &`
**Make sure to accept always**

Start the VNC Server `x11vnc -create -noshm`

Open VNC viewer and connect to **127.0.0.1:5900**