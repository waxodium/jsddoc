# JS-- Builtins and Standard Library

## Core Builtins

### syscall(num, args...)

- Number of arguments: 1 (syscall number) + up to 6 arguments
- Returns i32
- Used for OS system calls
- Example: `syscall(60, 1)` -> exit with code 1

```js
syscall(SYS_SOCKET, AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

### cat(...)

- Outputs arguments to stdout
- Can output numbers, strings, booleans
- Example: `cat(42); cat("hello");`

### alloc(n)

- Allocate n bytes of memory
- Returns pointer (i32 address)
- Must be paired with `free()`
- Example: `auto p = alloc(1024); free(p);`

### free(ptr)

- Deallocate previously allocated memory
- ptr must be result of alloc() or null
- Example: `free(p);`

### memcpy(dest, src, n)

- Copy n bytes from src to dest
- dest and src must be pointers
- n must be a number type
- Example: `memcpy(dst, src, 1024);`

### memset(dest, c, n)

- Set n bytes of dest to value c
- dest must be a pointer
- c must be a number type
- n must be a number type
- Example: `memset(buf, 0, 1024);`

## Standard Library (None)

The language explicitly excludes JavaScript built-ins.
No `console`, `arrays`, `objects`, `Math`, etc.
Only the above builtins are provided.
