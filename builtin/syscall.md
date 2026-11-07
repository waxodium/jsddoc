# The `syscall()` Builtin

`syscall()` invokes a Linux x86_64 system call directly.

```js
auto pid = syscall(39);
cat(pid);
```

The first argument is the system call number. Up to six more arguments are passed to the kernel. The result is returned as an `i32`.

`syscall()` is available on the Linux x86_64 target.

## Arguments

| Position | Meaning | Allowed types |
|----------|---------|---------------|
| 1 | system call number | `i32`, pointer |
| 2-7 | system call arguments | `i32`, pointer |

Numbers are converted to 64-bit integers. Pointer arguments are passed as raw addresses. The first argument is the system call number and should be numeric; pointers are only meaningful for the remaining arguments.

Strings, bytes, booleans, and other types are rejected at compile time. Pass a pointer to the data instead.

A call requires at least the system call number and accepts at most seven arguments in total.

## Example

`39` is `getpid` on Linux x86_64:

```js
auto pid = syscall(39);
cat(pid);
```

Extra arguments are allowed and passed through, so a call that takes none can still receive up to six:

```js
auto pid = syscall(39, 1, 2);
```

A pointer passes an address. This reads up to eight bytes from standard input into `value`:

```js
auto value = 0;
syscall(0, 0, &value, 8);
```

## Return value

The kernel's `rax` result is returned as a signed `i32`. On success it is the syscall's return value; on failure Linux returns `-errno`, which appears as a negative number:

```js
auto value = 0;
auto result = syscall(0, 0, &value, 8);
if (result < 0) cat("read failed");
```

## Errors

Calling without a system call number:

```js
syscall();
```

```
jsmm: expects at least arguments: syscall
```

Passing more than seven arguments:

```js
syscall(1, 2, 3, 4, 5, 6, 7, 8);
```

```
jsmm: expected type: syscall() accepts at most 7 arguments (syscall number plus 6 arguments)
```

Passing an unsupported argument type:

```js
auto text = "x";
syscall(1, 1, text, 1);
```

```
jsmm: expected type: syscall() arguments must be numbers or pointers, got `string'
```
