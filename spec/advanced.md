# JS-- Advanced Features

## Type Specialization

The language supports explicit integer type specialization via `i32<width, signed/unsigned>`:

- `i32<8, signed>` -- signed 8-bit integer
- `i32<16, signed>` -- signed 16-bit integer
- `i32<32, signed>` -- signed 32-bit integer (default)
- `i32<32, unsigned>` -- unsigned 32-bit integer
- `i32<64, signed>` -- signed 64-bit integer
- `i32<64, unsigned>` -- unsigned 64-bit integer

Type aliases can be created:

```
type i16 = i32<16, signed>;
type u32 = i32<32, unsigned>;
```

## String and Bytes Operations

```js
string s1 = "Hello, world!";
string s2 = "Hello";
string s3 = s1 + s2;       // Concatenation
cat(s1);                 // Output

bytes data = bytes "binary content";
cat(data.length);        // Length property
```

## Type Inquiry

```
typeof x -> "i32" | "f64" | "string" | "bytes" | "bool" | "auto"
```

## Aggregate Types

- Fixed-size arrays supported via type specialization
- No dynamic allocation of arrays in current implementation
