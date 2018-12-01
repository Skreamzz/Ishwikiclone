As said [here](https://github.com/tbodt/ish/wiki/FAQ#q-x-does-not-work) many programs could fail, so here is a list of programs known to be working (or not).

A list of what tbodt is working on is available [here](https://github.com/tbodt/ish/projects/7)

If you add a new test for a package, please add a line (same if package was already tested)

| Package name  | Is working ?  | Why ? / Note       | Device used (iOS version - iSH build)|
| :-------------|--------------:|:-------------------|:------------------------------------|
| `grep`, `head`, `cut`, `wc`|Yes|                   | iPad Air 2 (iOS 12.0.1 - 33)        |
| `ncurse`      | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `tput`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `irssi`       | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `ifconfig`    | Yes           | _ioctl 0x8912 failed: Invalid argument_  | iPad Air 2 (iOS 12.0.1 - 33)  |
| `ip`          | No            | _ip: socket(AF_NETLINK,3,0): Invalid argument_ (`ip route get 1`) | iPad Air 2 (iOS 12.0.1 - 33) |        
| `weechat`     | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `bash`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `zsh`         | Barely        | shows `\h:\w\$` with default config, _Bad system call_ after a command| iPad Air 2 (iOS 12.0.1 - 33)  |
| `nano`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `vim`         | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `vi`          | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `fish`        | ?             | Infinite loading   | iPad Air 2 (iOS 12.0.1 - 33)        |
| `neofetch`    | Yes           | Memory and Uptime and broken| iPad Air 2 (iOS 12.0.1 - 33)   |
| `screenfetch` | No            | _/proc/cpuinfo: No such file or directory_ | iPad Air 2 (iOS 12.0.1 - 33)  |
| `nodejs`      | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `npm`         | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `yarn`        | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `curl`        | Yes           | HTTPS too          | iPad Air 2 (iOS 12.0.1 - 33)  |
| `wget`        | Yes           | HTTPS too          | iPad Air 2 (iOS 12.0.1 - 33)  |
| `python3`     | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)  |
| `youtube-dl`  | ?             | Infinite loading   | iPad Air 2 (iOS 12.0.1 - 33)  |
| `cmus`        | No            | _bind: No such file or directory_ | iPad Air 2 (iOS 12.0.1 - 33)  |
| `ffmpeg`      | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)  |
| `emacs`       | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)  |
| `openssh` (client)| Yes       |                    | iPad Air 2 (iOS 12.0.1 - 31)  |
| `openssh` (server)| No        |                    | iPad Air 2 (iOS 12.0.1 - 31)  |

Testers:
jusdepatate