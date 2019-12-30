apk add alpine-baselayout alpine-keys  apk-tools busybox consolekit2 libc-utils lxdm sudo x11vnc xfce4 xfce4-terminal xorg-server xvfb xterm

cat /dev/location > /dev/null &

x11vnc -create -noshm

Open VNC viewer and connect to 127.0.0.1:5900