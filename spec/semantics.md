# JS-- Language Semantics

## Variables and Constants

### Declaration

```
auto x = 42;             // auto inference, initialized
i32<32, signed> x = 42;  // explicit type
u32 y = 42u;             // unsigned i32 (via type alias)
f64 pi = 3.14;           // floating-point
string s = "hello";      // text
bytes data = bytes "content";  // binary
bool flag = true;        // boolean
```

### Shadowing

- Inner scope variables shadow outer scope variables
- Type aliases don't create new scopes

## Scope Rules

- **Global scope**: declarations at file level
- **Function scope**: parameters and local variables
- **Block scope**: variables within `{}`
- `type` declarations have file scope

## Evaluation Order

- Left-to-right evaluation of function arguments
- Parentheses override default precedence
- Short-circuit: `&&` and `||` evaluate left-to-right, stopping when result is determined

## Control Flow

### If/Else

```js
if (condition) {
    // true branch
} else {
    // false branch
}
```

### While

```js
while (condition) {
    // body
    // break/continue supported
}
```

### For

```js
for (auto i = 0; i < 10; i = i + 1) {
    // body
}
```

### Break/Continue

- `break` exits enclosing loop or switch
- `continue` skips to next loop iteration

### Return

```js
auto add(a, b) {
    return a + b;
}
```

## Functions

### Function Declaration

```js
auto add(a, b) {
    return a + b;
}
```

### Parameters

- Functions accept any number of parameters
- Parameters are passed by value
- `auto` parameters infer type from argument

### Recursion

- Functions may call themselves recursively
- No tail call optimization guaranteed

### Closures

- Not currently supported in this version

## Memory Management

### alloc()

```js
auto p = alloc(1024);  // Allocate 1024 bytes
free(p);                   // Deallocate
```

### free()

```js
free(ptr);  // Deallocate previously allocated memory
```

### memcpy()

```js
memcpy(dest, src, n);  // Copy n bytes from src to dest
```

### memset()

```js
memset(dest, c, n);    // Set n bytes of dest to value c
```

## System Calls

### syscall()

```js
syscall(SYS_SOCKET, AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

- Number of arguments: 1 (syscall number) + up to 6 arguments
- Returns i32 file descriptor or error code

## Initialization Rules

- `auto` requires an initializer
- Explicit types require compatible initializer
- Uninitialized variables have undefined behavior
