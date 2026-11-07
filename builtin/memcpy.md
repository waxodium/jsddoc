# The `memcpy()` Builtin

`memcpy(dest, src, n)` copies `n` bytes from the memory area `src` to the memory area `dest`.

```js
auto dst = alloc(1024);
auto src = alloc(1024);
memcpy(dst, src, 1024);
```

## Arguments

| Position | Meaning | Allowed types |
|----------|---------|---------------|
| 1 | destination pointer | pointer |
| 2 | source pointer | pointer |
| 3 | number of bytes to copy | `i32` |

## Usage

```js
auto dst = alloc(1024);
auto src = alloc(1024);
memcpy(dst, src, 1024);
```

The source and destination memory areas must not overlap. For overlapping regions, behavior is undefined.

## Errors

- If `dest` or `src` is not a pointer type, a compile-time error is reported.
- If `n` is not a number type, a compile-time error is reported.
