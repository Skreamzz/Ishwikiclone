As said [here](https://github.com/tbodt/ish/wiki/FAQ#q-x-does-not-work) many programs do fail, so here is a list of programs known to be working (or not).

A list of what @tbodt is working on is available [here](https://github.com/tbodt/ish/projects/7)

If you add a new test for a package, please add a line (same if package was already tested). Feel free to update the device tested if the build is newer.

| Package name | Is working? | Notes | iSH version number |
|:-|:-|:-|:-|
| `grep`, `head`, `cut`, `wc` |Yes||33|
| `tput` |Yes||33|
| `irssi` |Yes|| 38 |
| `ifconfig` |No| `ioctl 0x8912 failed: Invalid argument` | 33 |
| `ip` | No | `ip: socket(AF_NETLINK,3,0): Invalid argument` (`ip route get 1`) | 33 |
| `weechat` | Yes ||53|
| `bash` | Yes || 33 |
| `zsh` | Yes | | 48 |
| `nano` | Yes ||33|
| `nvim` | Yes | |41|
| `vim` | Yes ||33|
| `vi` | Yes ||33|
| `fish` | Yes ||45|
| `neofetch` | Yes | Memory and Uptime and broken|52|
| `screenfetch` | No | _/proc/cpuinfo: No such file or directory_ |33|
| `nodejs` | No | Illegal instruction |41|
| `curl` | Yes | HTTPS too |33|
| `wget` | Yes | HTTPS too |33|
| `python3` | Yes ||33|
| `youtube-dl` | Yes | Very slow to start |35|
| `cmus` | No | Bad system call |52|
| `ffmpeg` | Yes | |35|
| `emacs` | Yes ||36|
| `openssh` (client)| Yes | |31|
| `openssh` (server)| Yes | Follow the [instructions on the wiki](Running-an-SSH-server) |45|
| `ps` | Yes ||34|
| `ruby` | Yes ||34|
| `irb` | Yes ||35|
| `gem` | Yes ||38|
| `go` | No | Requires the MMX instruction set. |34|
| `mate-session`| No | Bad system call |37|
| `tmux` | Yes ||53|
| `screen` | Yes |Detaches and reattaches!|53|
| `figlet` | Yes | |40|
| `uptime` | Yes | |40|
| `links` | Yes |  |40|
| `lynx` | Yes ||40|
| `gdb` | No | Segfault, socketcall 16 |40|
| `w3m` | Yes| Quits with `GC Warning: Couldn't read /proc/stat`` |40|
|`nmap`| No | `Assertion failed: res > 7 (nsock_pool.c: nsock_library_initialize: 307)` | 40|
|`&`, `bg`, `fg`, `jobs`|Yes||44|
|`mc`| Yes | F-keys don't work |48|
|`ed`| Yes | |52|
|`git`| Yes | |53|
|`mosh`| Yes | |54|
|`gcc `| Yes | |55|
|`gawk`| Yes | |55|
|`clang`| Yes | |55|

Testers:
jusdepatate, Mnpn, elchris414, JaquesBoum, wjid


## Test Requests

If you want a specific package to be tested, please add it here including special use cases you are interested in. This makes it easier to test meaningful things.

| Package name  | What to test / Note        | 
| :-------------|:---------------------------|
| `example`     | ...   |                   