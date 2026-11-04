# The `int()` Type

`int(...)` is a fixed-width integer type. `int` is a type annotation, not a runtime call.

```js
int count = 42;
int(8, unsigned) small = 200;
cat(count);
cat(small);
```

Plain `int` is `int(64, signed)`.

A value is converted to its declared integer type when it is stored, passed to a parameter, or returned from a function.

## Syntax

```js
int(8, unsigned) a = 255;
int(16, signed) b = -1000;
int(32, unsigned) c = 4000000000;
int(64, signed) d = -1;
int e = 7;
```

The first argument is the width in bits. The second argument is `signed` or `unsigned`. 
Both arguments are required when parentheses are used.

| Type | Range |
| --- | --- |
| `int(8, unsigned)` | 0 to 255 |
| `int(8, signed)` | -128 to 127 |
| `int(16, unsigned)` | 0 to 65535 |
| `int(16, signed)` | -32768 to 32767 |
| `int(32, unsigned)` | 0 to 4294967295 |
| `int(32, signed)` | -2147483648 to 2147483647 |
| `int(64, signed)`, `int` | -9223372036854775808 to 9223372036854775807 |

## Conversion

Conversion truncates toward zero, keeps the low `width` bits, and reinterprets the result as signed or unsigned.

| Assigned value | Type | Stored value |
| --- | --- | --- |
| `3.9` | `int` | `3` |
| `300` | `int(8, unsigned)` | `44` |
| `200` | `int(8, signed)` | `-56` |
| `400` | `int(8, signed)` | `-112` |
| `-1` | `int(8, unsigned)` | `0` |
| `4294967295` | `int(32, signed)` | `-1` |

Arithmetic is performed as `number`; the conversion happens only when the result is stored again:

```js
int(8, signed) value = 300;
value = value + 100;
cat(value);
```

`value` is `-112`.

## Parameters and returns

```js
number take(int(8, signed) value) {
    return value;
}
cat(take(200));

int(8, unsigned) wrap(number value) {
    return value;
}
cat(wrap(300));
```

`take(200)` is `-56`, and `wrap(300)` is `44`.

## Arrays

```js
int(16, signed) values[2] = [32767, 32768];
cat(values[0]);
cat(values[1]);
```

`values[0]` is `32767`, and `values[1]` is `-32768`.

## Representation

Integer values are carried as `number`, so `typeof` reports `number`:

```js
int(8, unsigned) value = 1;
cat(typeof(value));
```

Arithmetic and formatting therefore use number semantics. 
A 64-bit integer can name values beyond 2^53, but those are not exactly representable as `number`,
use a smaller width when exact bit patterns matter.
