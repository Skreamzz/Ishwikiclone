Run `apk add x11vnc xvfb xterm` to add all the required packages to run the VNC Server. 

Start backgrounding so we can connect with app not open`cat /dev/location > /dev/null &`
**Make sure to accept always**

Start the VNC Server `x11vnc -create -noshm`

Open VNC viewer and connect to **127.0.0.1:5900**