# The Monolith

> *"I inherited this codebase. I have no idea what's going on."*

---

## What is this?

Honestly? I'm not entirely sure.

What I **do** know:
- It's old. Like, really old.
- It's written in... C? Assembly? Both? Something else entirely? Yes.
- There are about 90,000 lines of code across hundreds of files
- There is exactly **one person on Earth** who fully understands this codebase, and they wrote it 30 years ago
- That person is not me

## What does it do?

It does... *things*. There's a main loop. There are platform-specific files for DOS, Windows, Linux, and Sun (yes, Sun). There's a virtual machine embedded inside it. There are custom binary file formats. There's hand-written x86 assembly for performance-critical paths.

It works. Nobody knows exactly how. Nobody wants to touch it. But it works.

## The current situation

- **Documentation**: You're looking at it
- **Tests**: None
- **CI/CD**: What's that?
- **Comments in code**: Mostly from the 90s, mostly cryptic
- **Build system**: Makefiles, Visual C++ project files, shell scripts  pick your adventure
- **Dependencies**: Some SDK from a company that no longer exists
- **Error handling strategy**: `Sys_Error("something bad happened")` and crash

## File structure (what I've figured out so far)

```
Monolith/
|-- 200+ .c files          # "the code"
|-- 100+ .h files          # "the other code"
|-- a bunch of .s files    # hand-written assembly, because why not
|-- Makefiles              # for Linux, Solaris, and vibes
|-- .mak files             # for MSVC, vintage edition
|-- .bat files             # "build scripts"
|-- .txt files             # the original README, from when README meant "please read me, I'm begging you"
+-- a folder called 'gas2masm'  # converts one type of assembly to another type of assembly, obviously
```

## Classic code patterns found in the wild

```c
// actual function signature from the codebase
void Sys_Error (char *error, ...)

// actual memory allocation strategy
parms.memsize = 8*1024*1024;  // 8 MB should be enough for anybody

// actual security model
sprintf(string, error);  // what could go wrong?
```

## Can we modernize this?

That's the plan. But first, someone needs to understand what *"this"* actually is.

Step 1: Figure out what we're dealing with

Step 2: ???

Step 3: Cloud-native microservices on Azure

We'll get there. Probably.

---

*If you're reading this and you wrote the original code  thank you, and also, we need to talk.*