# The `cat()` Builtin

`cat(...)` prints its arguments to standard output and ends the line with a newline. It accepts any number of arguments, including none.

```js
cat("Hello, ", "World");
```

```
Hello, World
```

No separator is inserted between arguments. Include spaces or punctuation explicitly:

```js
cat("a", "b");
```

```
ab
```

Calling it with no arguments prints only a newline:

```js
cat();
```

## Arguments

| Type | Printed as |
|---|---|
| `i32`, `f64` | decimal digits |
| `string` | the text, without quotes |
| `bytes` | the raw bytes, without quotes |
| `bool` | `true` or `false` |
| `null` | `null` |

Pointers and functions cannot be printed and are rejected at compile time.

## Numbers

Numbers print in decimal. Fractions show up to six digits, with trailing zeros removed:

```js
cat(3.14, " and ", 1.23456789);
```

```
3.14 and 1.234568
```

Fixed-width integers use the same representation:

```js
i32<32, signed> value = 200;
cat(value);
```

```
200
```

## Statements

Every call ends with a newline. `cat()` returns nothing and is intended to be used as a statement.

## Errors

Printing a pointer:

```js
i32 value = 1;
cat(&value);
```

```
jsmm: expected type: cat() cannot format a value of type `i32*'
```

Printing a function:

```js
auto one() {
    return 1;
}
cat(one);
```

```
jsmm: expected type: cat() cannot format a value of type `() -> i32'
```
