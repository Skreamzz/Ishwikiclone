Run `apk add x11vnc xvfb xterm` to add all the required packages to run the VNC Server. 


Start backgrounding so we can connect with app not open`cat /dev/location > /dev/null &`
**Make sure to accept always**

Start the VNC Server `x11vnc -create -noshm`

**Tip: add `-forever` to be able to quickly reconnect to a session if VNC disconnects**

Open VNC viewer and connect to **127.0.0.1:5900**