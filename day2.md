# Intro to C on Windows Day 2

We left off at running the OutputDebugStringA function, it printed it out to the
console.

Now what does the A mean in OutputDebugString:

- Well back in the day, Windows only used ASCII string. (If we search for ASCII
  in the internet, you will see an ASCII table)

So ASCII is a way to encode a certain value to a **Character**. Because, the
only thing we can deal with in computers are numbers, so what they did was
translate "letters" into "numbers".

You see if we ran the OutputDebugString without the A we will get this error:

```cpp
1>------ Build started: Project: test, Configuration: Debug Win32 ------
1>test.cpp
1>c:\users\tsp-windows\source\repos\test\test\test.cpp(5): error C2664: 'void OutputDebugStringW(LPCWSTR)': cannot convert argument 1 from 'const char [34]' to 'LPCWSTR'
1>c:\users\tsp-windows\source\repos\test\test\test.cpp(5): note: Types pointed to are unrelated; conversion requires reinterpret_cast, C-style cast or function-style cast
1>Done building project "test.vcxproj" -- FAILED.
========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ==========
```

Now let's get into Visual Studio, and use the debugger to figure this stuff out!
Well to put it simple, instead of running the program through Windows, we are
going to run the program through a tool that allows to find problems of it.

This is the **Start Debugging** button.

We are going to set a breakpoint, which tells the debugger to run the program
till a certain point of code (the breakpoint) and freeze it there.

To set a breakpoint we can either hit F9, and it will set one, at where our
cursor is, or we click on the gutter, then we will see a red dot appear, this is
the breakpoint of the program.

This is one way to set a breakpoint, we will learn about other ways soon.

Now we bring back the A in `OutputDebugStringA` and **Start Debugging**, we will
see a nice arrow on our breakpoint. So basically it went to that line, and it
freezed the program.

So let's close all the windows we have except for the Output and the Code, so we
can find out how to get the windows we want for debugging.

Well now, since we close everything, let us find out where all the windows in
Visual Studio, well you can find some windows in the View tab, but the one that
we are concerned with is the Debug>Windows tab, which houses all the debug
window of Visual Studio. The want we want is Watch, there are multiple, just
bring up 1.

You will see the following:

![Watch window](./assets/thewatchwindow.png)

This basically let's us put in a name of a variable or expression and Visual
Studio will spit out its value.

If we put our string into a variable like Foo:

```cpp
char *Foo = "This is the first thing we have actually printed"
```

![Foo Value](./assets/watchwindowwithfoo.png "Optional title")

Now we can see the actual value of Foo, the first is 84 -> 'T', this means that
in C, it will go through each of the letter and map it to those numbers.

Now why doesn't '\n' appear, this is because it is a special character called
"newline", they are there because it allows us to type things in that are not
built into the keyboard.

Why don't we just return? This is because the C syntax doesn't allow us to add
returns in strings. Now how do they type an actual backslash, we just type two
backslashes ("\\").

Now then if we look at the ASCII table, we might wonder why there are so many
returns, well different OSes uses different kinds of formatting to denote which
is a new line or not, so as an example in Windows, a newline is a 13 and 10, so
13 (\r) moves the cursor down and 10 (\n) moves to the beginning. This is also
called (CRLF).

Basically, most programs in Windows use this convention to denote the end of the
line. However on Unix, we only need to write "\n", for the end of a line.

So let's get back to the `OutputDebugStringA`, so string are just a list of
numbers as we saw, that are mapped via a table, as per the example above, it is
an ASCII table.

Back in the 16 bits days, everything in Windows was ASCII, but then, they found
Unicode, which is for many languages, where ASCII is only for English. In order
to do this though, they had to change all the API in Windows to use an encoding
called UTF-16 or Wide chars.

So if we call just `OutputDebugString` by itself, we don't get an error with
OutputDebugString, we get an error with OutputDebugStringW. So when Windows swap
from ASCII to using Unicode, they wanted all the APIs that they had to be
backwards compatable, so in this case they used something in C called a Macro.

A macro is C is way to replace string, so if we were to go inside the Code for
this we will see the following:

```cpp
#ifdef UNICODE
#define OutputDebugString  OutputDebugStringW
#else
#define OutputDebugString  OutputDebugStringA
#endif // !UNICODE
```

This is basically saying if we are in UNICODE mode use OutputDebugStringW, other
use OutputDebugStringA, so when we start a project in Visual Studio, we get a
choice between UNICODE and ASCII, defaulting to UNICODE, so that macro will
replace OutputDebugString with OutputDebugStringW. So we just do it manually, by
writing out `OutputDebugStringA`.
