The iSH App works with filesystems of Alpine Linux which are exportable and importable. As you know, installing and compiling software on iOS and iPadOS devices can take a lot of time. For example, `pip install numpy` may be stuck for at least an hour on building the Python wheel. Using Docker you can overcome these and other limitations such as installing large software like TexLive.

To install Docker, consult https://www.docker.com/get-started. Docker distinguishes between images (templates) and containers (filesystems created from images which you will work with). Images can be published and shared using the Docker Hub.
If you are already familiar with the shell in iSH but have never used Docker, it's not any more difficult.
You will need to use the following commands in your computer's terminal (please ignore the Docker Dashboard):  
`docker import -t [[image name]]:[[tag]] [[path to filesystem.tar.gz]]`  
`docker run --privileged -it --name [[container name]] [[image name]]:[[tag]] /bin/ash` (privileged access is required by some software)  
`docker cp [[container name]]:[[path to folder inside the container]] [[path to folder on your computer]]`


To import the iSH filesystem into Docker as an image, you need to run the first command, for example,  
`docker import -t econcz/x86-alpine-glibc:ish-import ~/Documents/default.tar.gz` (on MacOS or Linux)

Alternatively, you can download an already created image from the Docker Hub by typing  
`docker pull econcz/x86-alpine-glibc:ish-import`  
or, if you need a default iSH filesystem with GLibc (some software like Calibre or Miniconda / Anaconda requires it),  
`docker pull econcz/x86-alpine-glibc:ish-glibc-latest`.


To create a container, run the second command, for example,  
`docker run --privileged -it --name default econcz/x86-alpine-glibc:ish-import /bin/ash`  
`docker run --privileged -it --name glibc econcz/x86-alpine-glibc:ish-glibc-latest /bin/ash`

To be able to use **apk** to install software, you need to run these commands inside the container (the default iSH filesystem comes without a fully configured APK):  
`export ALPINE_VERSION=3.12`  or any other version that you wish to use  
`cp /etc/apk/repositories /tmp/repositories`  
`echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/main/" | tee /etc/apk/repositories`  
`echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/community/" | tee -a /etc/apk/repositories`

Now do what you wish to do with the filesystem and after you finish, run  
`mv /tmp/repositories /etc/apk/repositories `

The tricky part is to export the filesystem from the container back to iSH.  
The filesystem exported with the help of `docker export [[container name]] > ish-fs.tar.gz` may fail on importing it back into iSH because of the difference in **tar** versions on your computer and in the iSH App. **The typical error is linkname/pathname locale conversion from UTF-8**.

To avoid it, please run the following command inside the container:  
`tar czvf /tmp/ish-fs.tar.gz / --exclude=proc/* --exclude=sys/*`

then after you exit the container (you can simply type `exit`), run the last above-mentioned Docker command, for example,  
`docker cp default:/tmp/ish-fs.tar.gz ~/Documents/ish-fs.tar.gz` (on MacOS or Linux)  
`docker cp glibc:/tmp/ish-fs.tar.gz ~/Documents/ish-fs.tar.gz` (on MacOS or Linux)


That's it. Now you can import the filesystem into the iSH App and boot from them without issues!


**PS** If you are unsure about your computer security under Docker's privileged access, run the container without the `--privileged` flag.