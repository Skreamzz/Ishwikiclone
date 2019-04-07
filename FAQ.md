## Frequently Asked Questions

### Q: My favorite program does not work!
**A:** That’s not a question, but this is not surprising. Much of the emulation is still not finished, and many programs *will* fail. Do not hesitate to create [an issue](https://github.com/tbodt/ish/issues/new) if the specific program is not already on the [to-do list](https://github.com/tbodt/ish/projects/7), as it will be brought to the attention of the contributors, and they will (eventually) make it work. You can also check out [this page](https://github.com/tbodt/ish/wiki/What-works%3F) on the wiki where users actively test common programs.

### Q: When is the next TestFlight build coming out?
**A:** Sooner than it took for build 32 to come out. New builds are more frequent, and the app will be updated when something new has been added or fixed.

### Q: Is iSH 32-bit or 64-bit?
**A:** The app itself is a 64-bit ARM binary so that it can run on modern versions of iOS. iSH emulates x86_32 and as such can only run software compiled for this platform (specifically, it cannot currently run 64-bit ELF executables)