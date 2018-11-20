## The JIT
Possibly the most interesting thing written as part of iSH is the JIT. It's not actually a JIT since it doesn't target machine code. Instead, it generates an array of pointers to functions called gadgets, and each gadget ends with a tailcall to the next function; like the threaded code technique used by some Forth interpreters. The result is a speedup of roughly 3-5x compared to pure emulation.

Unfortunately, the decision was made to write nearly all of the gadgets in assembly language. This was probably a good decision with regards to performance (though we'll never know for sure), but a horrible decision with regards to readability, maintainability, and people's sanity.

Quoting the creator:
> The amount of bullshit I had to put up with from the compiler/assembler/linker is insane. It's like there's a demon in there that makes sure the code is sufficiently deformed, and if not, makes up stupid reasons why it shouldn't compile. In order to stay sane while writing this code, they had to ignore best practices in code structure and naming. You'll find macros and variables with such descriptive names as `ss`, `s` and `a`. Assembler macros nested beyond belief. And to top it off, there are almost no comments.

So, a warning: Long-term exposure to this code may cause loss of sanity, nightmares about GAS macros and linker errors, or any number of other debilitating side effects. This code is known to the State of California to cause cancer, birth defects, and reproductive harm.