# Installing R and any package from the CRAN
R is easy to install on iSH but compiling R packages will give you a headache. Trying to compile _stringr_ for instance will take hours on your iPhone.
The workaround is to compile the packages you want on another machine and to download the compiled version on iSH. This is surprisingly straight forward by using docker!

- First, check what is the current apk repository used by iSH. We will have to use the same on the other machine.
```
cat /etc/apk/repositories
```
Which would return 
```
http://dl-cdn.alpinelinux.org/alpine/v3.11/main
http://dl-cdn.alpinelinux.org/alpine/v3.11/community
```
on version 73.

- Download and install docker on another machine, by following instructions at https://www.docker.com

- Once docker installed, run the following commands to retrieve and run Alpine Linux 32 bits image:
```
docker pull i386/alpine  
docker run -it i386/alpine  
```

- In the docker image, ensure the same repository is used for apk. You can run the following commands:
```
echo "http://dl-cdn.alpinelinux.org/alpine/v3.11/main" > /etc/apk/repositories
echo "http://dl-cdn.alpinelinux.org/alpine/v3.11/community" >> /etc/apk/repositories
```

- In the docker image, run the following commands to install some of the apk required to compile R packages. The following are sufficient for dplyr for instance.
```
apk update
apk add R R-dev
apk add build-base gcc abuild binutils
apk add ccache
apk add linux-headers

apk add --no-cache cairo-dev libxmu-dev openjdk8-jre-base pango-dev perl tiff-dev tk-dev wget tar 
apk add --no-cache g++ gfortran icu-dev libjpeg-turbo libpng-dev make openblas-dev pcre-dev readline-dev xz-dev zlib-dev bzip2-dev curl-dev
apk add bash libsodium libsodium-dev libpq postgresql-dev mysql-dev
```

- Still in the docker image, run R and install the packages you want!
```
R
install.packages(c("dplyr","lubridate",...),dependencies=TRUE)
```
Before continuing you can read the logs and ensure packages were installed successfully by trying to use them. For instance:
```
library(dplyr)
```
Some packages might not compile because of missing dependencies. Copy/paste the error message on a search engine and you will know which apk shall be added to fix the problem.


- Now the goal is to copy the packages to iSH, which can be achieved in many different ways. For this exercice a FTP server has been set on the host machine running macOS, which is not covered by this tutorial.
Still in docker, archive all the packages that were installed:
```
cd /tmp
tar -zcvf libs.tar.gz /usr/lib/R/library
```
- Once done install a FTP client and push the tar file:
```
apk add lftp
lftp 192.168.0.9:2121
user anonymous
put libs.tar.gz
exit
```

This was the last step in the docker image. Now back to iSH.
- Install R on iSH:
```
apk add R
```
- Remove the libraries that were installed:
```
rm /usr/lib/R/library/* -r
```

- Install a FTP client and download the tar file to the tmp folder:
```
apk add lftp
cd /tmp
lftp 192.168.0.9:2121
user anonymous
get libs.tar.gz
exit
```

- Finally extract the files from the archive:
```
tar -zxf libs.tar.gz --directory /
```

This is done. Now you can run R and use the packages you compiled before.

# Packages that were tested
| Package name | Is working? | Notes | iSH version number |
|:-|:-|:-|:-|
| stringr |Yes||73|
| lubridate |Yes||73|
| dplyr |Yes||73|
| purrr |Yes||73|
| sqldf |Yes||73|








