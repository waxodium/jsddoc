# JS-- Type System

## Type Inventory

| Type | Kind | Description |
|------|------|-------------|
| `bool` | Boolean | True/false values |
| `i32<32, signed>` | Integer | Signed 32-bit integer |
| `i32<32, unsigned>` | Integer | Unsigned 32-bit integer |
| `f64` | Floating-point | 64-bit floating-point |
| `string` | Text | UTF-8 string literal |
| `bytes` | Binary | Raw byte sequence |
| `auto` | Inferred | Type inferred from initializer |
| `void` | Void | Void return type |

## Type Syntax

```
i32<32, signed>    -- signed 32-bit integer
i32<32, unsigned>  -- unsigned 32-bit integer
f64                -- 64-bit floating-point
string             -- text sequence
bytes              -- raw binary data
auto               -- inferred from initializer
void               -- void type
```

## Type Specialization

The language supports explicit integer type specialization via `i32<width, signed/unsigned>`:

- `i32<8, signed>` -- signed 8-bit integer
- `i32<16, signed>` -- signed 16-bit integer
- `i32<32, signed>` -- signed 32-bit integer (default)
- `i32<32, unsigned>` -- unsigned 32-bit integer
- `i32<64, signed>` -- signed 64-bit integer
- `i32<64, unsigned>` -- unsigned 64-bit integer

```
i32<32, signed>    -- signed 32-bit integer literal
i32<32, unsigned>  -- unsigned 32-bit integer literal
```

## Type Aliases

```
type i32 = i32<32, signed>;     // Define alias
i32 x = 42;                     // Use alias
```

Additional examples:

```
type i16 = i32<16, signed>;
type u32 = i32<32, unsigned>;
type byte = i32<8, unsigned>;
```

## Type Inference

`auto` infers the type from the initializer:

| Declaration | Inferred Type |
|-------------|---------------|
| `auto x = 42;` | `i32` |
| `auto x = 3.14;` | `f64` |
| `auto x = true;` | `bool` |
| `auto x = "hello";` | `string` |
| `auto x = bytes "content";` | `bytes` |

## Type Compatibility

- `i32<32, signed>` is compatible with `i32` (type alias)
- `f64` is compatible with `auto` when initialized with f64 literal
- `string` and `bytes` are distinct types
- No implicit numeric promotions -- explicit types required

## Literals

### Integer Literals

```
42       -- decimal integer
0xFF     -- hexadecimal integer
0b1010   -- binary integer (if supported)
```

### Floating-Point Literals

```
3.14     -- decimal floating-point
1.5e10   -- scientific notation (if supported)
```

### Boolean and Null Literals

```
true, false  -- boolean values
null         -- null value
```

## Type Inquiry

```
typeof x -> "i32" | "f64" | "string" | "bytes" | "bool" | "auto"
```
