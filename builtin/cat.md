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
| --- | --- |
| `number`, `byte`, `int` | decimal digits |
| `string` | the text, without quotes |
| `bytes` | the raw bytes, without quotes |
| `boolean` | `true` or `false` |
| `null` | `null` |
| `array` | elements in `[...]`, separated by `, ` |
| `union` | the active value |

Pointers, objects, and functions cannot be printed and are rejected at compile time. Arrays follow the same rule for their elements.

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
int(8, signed) value = 200;
cat(value);
```

```
-56
```

## Arrays

```js
cat([1, 2, 3]);
cat([]);
cat([[1, 2], [3]]);
cat(["x", "y"]);
```

```
[1, 2, 3]
[]
[[1, 2], [3]]
[x, y]
```

Elements are separated by `, `, and strings inside arrays print without quotes.

## Statements

Every call ends with a newline. `cat()` returns `undefined` and is intended to be used as a statement.

## Errors

Printing a pointer:

```js
number value = 1;
cat(&value);
```

```
jsmm: expected type: cat() cannot format a value of type `number*'
```

Printing an object:

```js
cat({ a: 1 });
```

```
jsmm: expected type: cat() cannot format a value of type `struct ObjectLiteral { a: number }'
```

Printing an array of pointers:

```js
number value = 1;
cat([&value]);
```

```
jsmm: expected type: cat() cannot format a value of type `number*[]'
```

Printing a function:

```js
number one() {
    return 1;
}
cat(one);
```

```
jsmm: expected type: cat() cannot format a value of type `() -> number'
```
