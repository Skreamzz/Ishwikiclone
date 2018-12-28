As said [here](https://github.com/tbodt/ish/wiki/FAQ#q-x-does-not-work) many programs do fail, so here is a list of programs known to be working (or not).

A list of what @tbodt is working on is available [here](https://github.com/tbodt/ish/projects/7)

If you add a new test for a package, please add a line (same if package was already tested). Feel free to update the device tested if the build is newer.

| Package name | Is working? | Notes | iSH version number |
|:-|-|:-|:-|
| `grep`, `head`, `cut`, `wc` |Yes||33|
| `tput` |Yes||33|
| `irssi` |Yes|| 38 (unreleased) |
| `ifconfig` |No| `ioctl 0x8912 failed: Invalid argument` | 33 |
| `ip` | No | `ip: socket(AF_NETLINK,3,0): Invalid argument` (`ip route get 1`) | 33 |
| `weechat` | No | Starts but fails  |35|
| `bash` | Yes || 33 |
| `zsh` | Barely | `Bad system call` after running a command| 33 |
| `nano` | Yes ||33|
| `nvim` | No | _Bad system call_ |34|
| `vim` | Yes ||33|
| `vi` | Yes ||33|
| `fish` | Yes ||38 (unreleased)|
| `neofetch` | Yes | Memory and Uptime and broken|33|
| `screenfetch` | No | _/proc/cpuinfo: No such file or directory_ |33|
| `nodejs` | No | _Bad system call_ |33|
| `npm` | No | _Bad system call_ |33|
| `yarn` | No | _Bad system call_ |33|
| `curl` | Yes | HTTPS too |33|
| `wget` | Yes | HTTPS too |33|
| `python3` | Yes ||33|
| `youtube-dl` | Yes | Very slow to start |35|
| `cmus` | No | _bind: No such file or directory_ |33|
| `ffmpeg` | Yes | |35|
| `emacs` | Yes ||36|
| `openssh` (client)| Yes | |31|
| `openssh` (server)| No | |31|
| `ps` | Partially | Runs, but /proc is empty. |34|
| `ruby` | Yes ||34|
| `irb` | Yes ||35|
| `gem` | Yes ||38|
| `go` | No | Says `This program can only be run on processors with MMX support. |34|
| `mate-session`| No. | _Bad system call_. |37|
| `tmux` | No | _lost server_ |37|
| `figlet` | Yes | |40|
| `uptime` | Yes | |40|
| `links` | Yes |  |40|
| `lynx` | Yes ||40|
| `w3m` | Yes, quits with `GC Warning: Couldn't read /proc/stat` ||40|

Testers:
jusdepatate, Mnpn, elchris414, JaquesBoum


## Test Requests

If you want a specific package to be tested, please add it here including special use cases you are interested in. This makes it easier to test meaningful things.

| Package name  | What to test / Note        | 
| :-------------|:---------------------------|
| `example`     | ...   |                   