
 ![](https://photos.smugmug.com/Ish/i-2MXm8VF/0/384caaa2/S/iSHPHONE-S.png) 


As said [here](https://github.com/tbodt/ish/wiki/FAQ#q-x-does-not-work) many programs do fail, so here is a list of programs known to be working (or not).

If you add a new test for a package, please add a line (same if package was already tested). Feel free to update the device tested if the build is newer.

| Package name | Status | Notes | iSH version number | Method |
|:-|:-|:-|:-|:-|
| `apt`,`apt-*` | No | Illegal instruction | 74 |
| `arp` | No | can't open '/proc/net/arp': No such file or directory | 73 |
| `bash` | Yes || 33 |
| `brew` (tigerbrew) | No | `Error: Cannot find a vendored version of curl for your i686 processor on Linuxbrew! Error: Failed to install vendor Curl. `| 74 |
| `cmatrix` | Yes | | | apk add cmatrix |
| `cmus` | No | Bad system call |52|
| `cheat.sh` | Partially workling |  | | git clone |
| `clang` | Yes | |55|
| `curl` | Yes | HTTPS too |33| apk add curl |
| `ddate` | Yes | | 1.0.1 |
| `dillo` | Partially working | Follow the [instructions ](https://github.com/ish-app/ish/wiki/Running-a-VNC-Server) to install VNC server. Requires fonts-noto to be installed. Some website don’t work |67|
| `dig`| No | Runtime check fails but you can use `drill` as a drop-in replacement | 1.0.1 |
| `drill`| Yes | | 1.0.1 |
| `dumb-init` | Yes | | 74 |
| `emacs` | Yes |works recursively in `M-x term` !|36|
| `figlet` | Yes | |40|
| `fish` | Yes ||45|
| `gawk`| Yes | |55|
| `gdb` | No | Segfault, socketcall 16 |40|
| `git`| Yes | |53| apk add git |
| `gcc `| Yes | |55|
| `grep`, `head`, `cut`, `wc` |Yes||33|
| `gem` | Yes ||38|
| `go` | Yes | |67|
| `gnome-calculator`| Yes | Will illegal instruction after first use, need to delete configuration. | 76 |
| `irssi` |Yes|| 38 |
| `ifconfig` |No| `ioctl 0x8912 failed: Invalid argument` | 33 |
| `ip` | No | `ip: socket(AF_NETLINK,3,0): Invalid argument` | 33 |
| `init` (busybox) | Yes | | 74 |
| `weechat` | Yes ||53|
| `nvim` | Yes | |41|
| `vim` | Yes ||33|
| `vi` | Yes ||33|
| `screenfetch` | No | _/proc/cpuinfo: No such file or directory_ |33|
| `wget` | Yes | HTTPS too |33| apk add wget |
| `python3` | Yes ||33|
| `ps` | Yes ||34|
| `youtube-dl` | Yes | Very slow to start |35|
| `ffmpeg` | Yes | |35|
| `openssh` (client)| Yes | |31| apk add openssh |
| `openssh` (server)| Yes | Follow the [instructions on the wiki](Running-an-SSH-server) |45|
| `openssh` (server)| No | tested on Ubuntu 18.04.5 `illegal instruction at 0xf79f981d: 0f de d8 66 0f de e2 66 `| 74 |
| `resolvconf` | Yes | Tested on Ubuntu 18.04.5 | 74 |
| `ruby` | Yes ||34|
| `irb` | Yes ||35|
| `mate-session`| No | Bad system call |37|
| `tmux` | Yes ||53|
| `uptime` | Yes | |40|
| `links` | Yes |  |40|
| `lynx` | Yes ||40|
| `w3m` | Yes| Quits with `GC Warning: Couldn't read /proc/stat` |40|
| `&`, `bg`, `fg`, `jobs`|Yes||44|
| `ed`| Yes | |52|
| `php`| Yes | |65|
| `php (extensions)`| Yes | |65|
| `perl`| Yes | |65|
| `openssl`| Yes | Even signing certificates work perfectly fine |65|
| `dpkg`| No | Illegal Instruction  |73|
| `wine`| No | Illegal Instruction when trying to run any program | 73 |
| `lftp`| Yes | | 73 |
| `plistutil` | Yes | | 74 |
| `img4tool` | Yes | | 74 |
| `man-pages` | Yes | | | apk add mandoc man-pages less less-doc |
| `metadelta` | Yes | | | git clone |
| `metasploit-framework` | Yes | launch with `msfconsole -n` | 78 |
| `Midnight Commander`| Yes | F-keys don't work |48| apk add mc |
| `mosh`| Yes | |54|
| `nano` | Yes ||33|
| `neofetch` | Yes ||52|
| `nautilus`| Yes | Will illegal instruction after first use, need to delete configuration. | 76 |
| `nmap`| No | Assertion failed | 40|
| `node` | Yes || 73 |
| `R`| Yes | For installing CRAN packages follow the [instructions on the wiki](Installing-R-and-any-package-from-the-CRAN) | 73 |
| `Ranger` | Yes | | | git glone | 
| `runit`| No | | 74 |
| `screen` | Yes |Detaches and reattaches!|53|
| `sddm`| No | Illegal Instruction| 74 |
| `spreadsheet calculator` | unsure | | | "apk add ncurses-dev" & "git clone <link>" |
| `sshfs`| No | fuse: device not found, try 'modprobe fuse' first | 74 |
| `stunnel3`| Yes | perl needs to be installed |65|
| `systemd`| No | | 74|
| `tput` |Yes||33|
| `plasma-desktop`| No | Illegal Instruction| 74 |
| `openrc`| Yes | both the openrc command and init system works | 74 |
| `dpkg` (busybox) | Yes | compile with -mtune=i386 | 74 |
| `lighttpd` | No | `(stat_cache.c.601) server.stat-cache-engine can be one of "disable", "simple", but not: fam` | 76 |
| `jq`| Yes | | 76 |
| `wptc-track`| Yes | | 78 |
| `zsh` | Yes | | 48 |

Testers:
jusdepatate, Mnpn, elchris414, JaquesBoum, wjid, DiscordDigital, Linux, assfugil, ReedSan


## Test Requests

If you want a specific package to be tested, please add it here including special use cases you are interested in. This makes it easier to test meaningful things.

| Package name  | What to test / Note        | 
| :-------------|:---------------------------|
| `example`     | ...   |   
| `docker-ce`   | For running webapps |   
| `code-server`   | To run vs code in browser |   
| `ghc`         | Haskell file compiling     |
