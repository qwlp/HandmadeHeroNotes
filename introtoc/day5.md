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

       Memory
     Intel Encoding   <->     I(Instruction)CACHE     <->      CPU

VMAS          
Page (rwx) (STACK) The stack can grow
Page (rwx) (STACK)
Page (rwx) (STACK)
Page (rwx) (STACK)
Page (rwx) (STACK)
```

Operators lets you do interesting stuff in the program. `- + = * /` no ^ you'd
need to call pow(num)

Operators also have precedence, * first, + and all that like math.
