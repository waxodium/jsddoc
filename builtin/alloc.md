# The `alloc()` Builtin

`alloc(n)` allocates `n` bytes of memory and returns a pointer to the allocated block.

```js
auto p = alloc(1024);
```

## Arguments

| Position | Meaning | Allowed types |
|----------|---------|---------------|
| 1 | number of bytes to allocate | `i32` |

## Return value

Returns a pointer (i32 address) to the newly allocated memory block. The memory is uninitialized.

## Usage

```js
auto p = alloc(1024);
// use p...
free(p);
```

The allocated memory must be paired with `free()` to avoid memory leaks.

## Errors

- If `n` is not a number type, a compile-time error is reported.
- If allocation fails at runtime, the behavior is target-dependent.
