# The `free()` Builtin

`free(ptr)` deallocates a previously allocated block of memory.

```js
auto p = alloc(1024);
free(p);
```

## Arguments

| Position | Meaning | Allowed types |
|----------|---------|---------------|
| 1 | pointer to deallocate | pointer (result of `alloc()` or `null`) |

## Usage

```js
auto p = alloc(1024);
// use p...
free(p);
```

`ptr` must be the result of a previous `alloc()` call, or `null`. Passing any other value is undefined behavior.

## Errors

- If `ptr` is not a pointer type, a compile-time error is reported.
- Double-free or freeing invalid pointers is undefined behavior.
