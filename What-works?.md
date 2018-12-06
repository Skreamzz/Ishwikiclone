As said [here](https://github.com/tbodt/ish/wiki/FAQ#q-x-does-not-work) many programs do fail, so here is a list of programs known to be working (or not).

A list of what @tbodt is working on is available [here](https://github.com/tbodt/ish/projects/7)

If you add a new test for a package, please add a line (same if package was already tested). Feel free to update the device tested if the build is newer.

| Package name  | Is working ?  | Why? / Note        | Device used (iOS version - iSH build)|
| :-------------|--------------:|:-------------------|:------------------------------------|
| `grep`, `head`, `cut`, `wc`|Yes|                   | iPad Air 2 (iOS 12.0.1 - 33)        |
| `ncurse`      | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `tput`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `irssi`       | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `ifconfig`    | No            | _ioctl 0x8912 failed: Invalid argument_  | iPad Air 2 (iOS 12.0.1 - 33)  |
| `ip`          | No            | _ip: socket(AF_NETLINK,3,0): Invalid argument_ (`ip route get 1`) | iPad Air 2 (iOS 12.0.1 - 33) |        
| `weechat`     | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `bash`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `zsh`         | Barely        | shows `\h:\w\$` with default config, _Bad system call_ after a command| iPad Air 2 (iOS 12.0.1 - 33)  |
| `nano`        | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `vim`         | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `vi`          | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)        |
| `fish`        | No            | Infinite loading, can't stop | iPhone X (iOS 12.1.1 - 34)        |
| `neofetch`    | Yes           | Memory and Uptime and broken| iPad Air 2 (iOS 12.0.1 - 33)   |
| `screenfetch` | No            | _/proc/cpuinfo: No such file or directory_ | iPad Air 2 (iOS 12.0.1 - 33)  |
| `nodejs`      | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `npm`         | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `yarn`        | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)        |
| `curl`        | Yes           | HTTPS too          | iPad Air 2 (iOS 12.0.1 - 33)  |
| `wget`        | Yes           | HTTPS too          | iPad Air 2 (iOS 12.0.1 - 33)  |
| `python3`     | Yes           |                    | iPad Air 2 (iOS 12.0.1 - 33)  |
| `youtube-dl`  | Yes           | Very slow, cannot merge audio and video (ffmpeg issue) | iPhone X (iOS 12.1.1 - 34)  |
| `cmus`        | No            | _bind: No such file or directory_ | iPad Air 2 (iOS 12.0.1 - 33)  |
| `ffmpeg`      | Partially     | `youtube-dl` can't merge audio and video | iPad Air 2 (iOS 12.0.1 - 33)  |
| `emacs`       | No            | _Bad system call_  | iPad Air 2 (iOS 12.0.1 - 33)  |
| `openssh` (client)| Yes       |                    | iPad Air 2 (iOS 12.0.1 - 31)  |
| `openssh` (server)| No        |                    | iPad Air 2 (iOS 12.0.1 - 31)  |
| `ps`          | Partially     | Runs, but /proc is empty. | iPhone X (iOS 12.1.1 - 34)  |
| `ruby`        | Yes           | Tested with simple script. | iPhone X (iOS 12.1.1 - 34)  |
| `irb`         | No            | Slow, displays Ruby error | iPhone X (iOS 12.1.1 - 34)  |
| `gem`         | Barely        | Runs, `gem install` gives `Bad file descriptor`. | iPhone X (iOS 12.1.1 - 34)  |

Testers:
jusdepatate, Mnpn