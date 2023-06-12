**These instructions assume you are running as root in the default iSH root Filesystem.  If this is not the case then some things will fail.  Most notably, if you are running the AOK iSH root FS you will be the 'ish' user by default.  In recent versions of AOK there are two scripts to assist you.  One is 'enable_vnc' which will essentially do everything listed here except what is in the the final script.  The other is 'vnc_start' which is essentially the last script included in this tutorial.  If these scripts are not present then 'sudo su -' to become root before following the instructions below.**


# First, install needed software.  I assume the [i3 window manager](https://i3wm.org/docs/) will be used to keep things simple.

`apk add x11vnc x11vnc-doc xvfb xterm xorg-server xf86-video-dummy i3wm i3status i3lock xdpyinfo xdpyinfo-doc i3wm-doc i3lock-doc i3status-doc ttf-dejavu`

## Next create needed files and directories.

    mkdir -p /etc/X11/xorg.conf.d

## Create X11 headless config
    cat <<HERE > /etc/X11/xorg.conf.d/10-headless.conf
    Section "Monitor"
            Identifier "dummy_monitor"
            HorizSync 28.0-80.0
            VertRefresh 48.0-75.0
            DisplaySize  250 174    # In millimeters, iPad gen 7 & 8
    EndSection

    Section "Device"
            Identifier "dummy_card"
            VideoRam 256000
            Driver "dummy"
    EndSection

    Section "Screen"
            Identifier "dummy_screen"
            Device "dummy_card"
            Monitor "dummy_monitor"
            SubSection "Display"
               depth 24
               Modes "1024x768"  # Works OK on ~10 inch iPad's
     #          Modes "1280x1024"  # Likely to work on larger iPad
            EndSubSection
    EndSection
    HERE


## Create a place for logs to go.
    if [ ! -e /root/i3logs ]; then
       mkdir /root/i3logs
    fi

## Create default .xinitrc file.
    cat <<THERE > /root/.xinitrc
    xrdb -merge ~/.Xresources
    xterm -geometry 80x50+494+51 &
    xterm -geometry 80x20+494-0 &
    exec i3 -V >> /root/i3logs/i3log-$(date +'%F-%k-%M-%S') 2>&1
    THERE

## Create .Xresources file

    cat <<EVERYWHERE > /root/.Xresources
    Xft.dpi: 264
    xterm*VT100.Translations: #override \
        Ctrl <Key> minus: smaller-vt-font() \n\
        Ctrl <Key> plus: larger-vt-font() \n\
        Ctrl <Key> 0: set-vt-font(d)
    EVERYWHERE

## That is the prep work done

# The following script can be used to start vnc

    #!/bin/ash
    #
    # Stupidly simple script to start vnc.  

    CHECK=`ps -o args | grep "{startx} /bin/sh /usr/bin/startx" | wc -l`

    # Only run once.  The grep causes CHECK to equal 1
    if [ $CHECK -eq 1 ]; then # Nothing running, clear stale locks
       rm -rf /tmp/.X* 
    else
       echo "$0 is already running.  We're done here."
       exit 1
    fi
    
    # See if location services are running already.  
    # Having them running reduces the odds of iSH getting
    # killed while in the background.
    CHECK=`ps -o args | grep "cat /dev/location" | wc -l`

    # Only run once.  The grep causes CHECK to equal 1
    if [ $CHECK -eq 1 ]; then
       cat /dev/location > /dev/null &
    fi

    startx &
    x11vnc -display :0 -noshm -forever & 

# --------------- Original Instructions Below -------------------
Run `apk add x11vnc xvfb xterm` to add all the required packages to run the VNC Server. 


Start backgrounding so we can connect with app not open`cat /dev/location > /dev/null &`
**Make sure to accept always**

Start the VNC Server `x11vnc -create -noshm`

**Tip: add `-forever` to be able to quickly reconnect to a session if VNC disconnects**

Open VNC viewer and connect to **127.0.0.1:5900**

You should get greeted with a weird and definetely not good looking terminal.
Let's make that a little more useful.

First, set up a headless xorg-server. For that, install the following packages: `apk add xorg-server xf86-video-dummy`.
Now you have to configure the xserver to run headless, so without a display. Create a new file at `/etc/X11/xorg.conf.d` called `10-headless.conf` and add the following content:

```
Section "Monitor"
        Identifier "dummy_monitor"
        HorizSync 28.0-80.0
        VertRefresh 48.0-75.0
        Modeline "1920x1080" 172.80 1920 2040 2248 2576 1080 1081 1084 1118
EndSection

Section "Device"
        Identifier "dummy_card"
        VideoRam 256000
        Driver "dummy"
EndSection

Section "Screen"
        Identifier "dummy_screen"
        Device "dummy_card"
        Monitor "dummy_monitor"
        SubSection "Display"
        EndSubSection
EndSection
```

Now you can install your window manager. For this tutorial, we're going to use i3wm. It's a tiling window manager with good configuration options. Run `apk add i3wm i3status i3lock` to install the required packages. The last step before starting our GUI is to specify the window manager that we want to use. Create a `.xinitrc` file in your home directory and add the following line:

```
exec i3
```

You need to run two commands side by side. The first one to start the headless GUI and the second one to start the vnc server.
To accomplish this, you can use a multiplexer like tmux or add the commands to the background with `&`.

To start the xserver, run `startx`. Then start the vnc server with `x11vnc -display :0 -noshm`.
Log in with your vnc client and you're ready to go. But don't expect a very good performance.