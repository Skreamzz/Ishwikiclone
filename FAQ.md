## Frequently Asked Questions

### Q: My favorite program doesn't work!
**A:** That’s not a question, but this is not surprising. Much of the emulation is still not finished, and many programs *will* fail. Do not hesitate to create [an issue](https://github.com/tbodt/ish/issues/new) if the specific program is not already on the [to-do list](https://github.com/tbodt/ish/projects/7), as it will be brought to the attention of the contributors, and they will (eventually) make it work. You can also check out [this page](https://github.com/tbodt/ish/wiki/What-works%3F) on the wiki where users actively test common programs.

### Q: When is the next TestFlight build coming out?
**A:** Sooner than it took for build 32 to come out. New builds are more frequent, and the app will be updated when something new has been added or fixed.

### Q: Is iSH 32-bit or 64-bit?
**A:** The app itself is a 64-bit ARM binary so that it can run on modern versions of iOS. iSH emulates x86_32 and as such can only run software compiled for this platform (specifically, it cannot currently run 64-bit ELF executables). 

### Q: Why does iSH not emulate ARM or some other architecture?
**A:** Mostly because x86 was what [@tbodt](https://github.com/tbodt) was comfortable with at the time. Using x86 also has the added benefit of letting us access to the rich set of software that’s already been built for this platform. Performance-wise the choice of architecture is not all that important, since the code is being emulated anyways (that is, using ARM wouldn’t actually help much).

### Q: Why does iSH emulate at all? Can't it use a JIT compiler, or virtualization?
**A:** iOS devices lack support for hardware virtualization, and even if such a thing did exist it would need to be exposed to applications before it could be used. Generating code on the fly, which is required for JIT compilation, is not intended for use by third-party applications and such a technique requires entitlements that cannot be used when uploading to App Store Connect (as is necessary for distribution via TestFlight).

### Q: I lost access to the TestFlight?
**A:** That might be because we hit the limit of testers, at 10,000, so we did some house cleaning and removed testers who have either been inactive, or haven't updated. If needed [you can join the TestFlight again.](https://testflight.apple.com/join/97i7KM8O)

### Q: How do you know what an instruction does?
**A:** Generally we look [here](https://www.felixcloutier.com/x86/).

You can look up the instructions by number [here](https://github.com/torvalds/linux/blob/master/arch/x86/entry/syscalls/syscall_32.tbl)

### Q: iSH looks cool, but I'm not sure what to use it for. What can I do in iSH?
**A:** Most things you can do in a headless Linux environment. A few ideas:
- Connect to telnet, SSH, and SFTP servers
- Edit files with `vim`, `nano`, or `emacs`
- Work with `git` repositories
- Write and run programs in Python, C, C++, Bash, and many more languages
- Edit text files that other editors might not support, like `.json` files
- Convert images with `magick`/`gm` and `vipsthumbnail`
- Test networks with `ping`, `nslookup`, `traceroute` and `nc`
- Chat on IRC with `irssi`, `weechat`
- Play text-based games like `nethack` and the classic `advent` (Colossal Cave Adventure)
- Read and download the sources of web pages with `curl` and `wget`
- Use `gpg` to encrypt, decrypt, sign, and verify the signatures of files
- Create and extract `tar` and `zip` archives

### Q: Where can I get help for using [malicious tool]?
**A:** [This link](https://idiot.razor0.repl.co/) might be useful.