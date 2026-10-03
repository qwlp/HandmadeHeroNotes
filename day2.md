# Day 2

Opening a Win32 Window

We start off with a WNDCLASS:

```c++
typedef struct tagWNDCLASSW {
  UINT      style;
  WNDPROC   lpfnWndProc;
  int       cbClsExtra;
  int       cbWndExtra;
  HINSTANCE hInstance;
  HICON     hIcon;
  HCURSOR   hCursor;
  HBRUSH    hbrBackground;
  LPCWSTR   lpszMenuName;
  LPCWSTR   lpszClassName;
} WNDCLASSW, *PWNDCLASSW, *NPWNDCLASSW, *LPWNDCLASSW;
```

In C++ you can have:

```c++
struct foo
{
  int X;
};
foo Foo;
```

In C though you would need:

```c
struct foo
{
  int X;
};
struct foo Foo;
```

That's a bit annoying, this is where the typedef comes in:

```c
struct foo
{
	int X;
};
typedef struct foo foo;
```

This is how to zero init all the fields in a structs:

```c
WNDCLASS WindowClass = {};
```
