# Intro to C Day 5

```
                    Lib
                     |
                     v
Code -> Compiler -> Obj -> Linker -> EXE

# EXE has:
                      Virtual Address
                       Memory
Header
Fixup Table
Intercode     ->      Intercode
                      Windows Code

VMAS (Virtual Memory Address Space) can be 4096b or 64kb

VMAS                                    Page Table
Page (rwx)            ->                Place in Memory 
Page (rwx)
Page (rwx)

If ran out, it writes to disk and updates perm in the page.
```
