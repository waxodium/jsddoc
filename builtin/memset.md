# The `memset()` Builtin

`memset(dest, c, n)` sets the first `n` bytes of the memory area `dest` to the value `c`.

```js
auto buf = alloc(1024);
memset(buf, 0, 1024);
```

## Arguments

| Position | Meaning | Allowed types |
|----------|---------|---------------|
| 1 | destination pointer | pointer |
| 2 | fill value | `i32` |
| 3 | number of bytes to set | `i32` |

## Usage

```js
auto buf = alloc(1024);
memset(buf, 0, 1024);
```

## Errors

- If `dest` is not a pointer type, a compile-time error is reported.
- If `c` or `n` is not a number type, a compile-time error is reported.
