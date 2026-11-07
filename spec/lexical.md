# JS-- Lexical Specification

## Keywords (Authorized)

`break`, `else`, `for`, `if`, `return`, `switch`, `while`, `type`, `auto`, `void`, `i32`, `struct`

## Removed Keywords (per specification)

- `number` -- replaced by explicit `i32`/`f64` types
- `const` -- not in authorized set

## Authorized Types

| Type | Kind | Description |
|------|------|-------------|
| `bool` | Boolean | True/false values |
| `i32<width, signed/unsigned>` | Integer | Explicit integer type specialization |
| `f64` | Floating-point | 64-bit floating-point |
| `string` | Text | UTF-8 string literal |
| `bytes` | Binary | Raw byte sequence |
| `auto` | Inferred | Type inferred from initializers |
| `void` | Void | Void functions |

## Punctuators

`>>>`, `>>=`, `&&`, `||`, `??`, `++`, `--`, `<=`, `>=`, `==`, `!=`, `>>`, `<<`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `**`, `{`, `}`, `(`, `)`, `[`, `]`, `.`, `;`, `,`, `<`, `>`, `+`, `-`, `*`, `/`, `%`, `=`, `!`, `~`, `^`, `&`, `|`, `:`

## Tokenization

- `i32` is tokenized as a **Keyword**
- All other identifiers are tokenized as `TokenKind::Identifier`
- `??` (nullish coalescing) is present in the lexer but the parser rejects it
- `**` (power) operator is removed from grammar

## Whitespace and Comments

- Whitespace: spaces, tabs, `\v`, `\f`, `\r`, `\n` are separators
- Comments: Single-line `//` style only
- Case-sensitive matching

## Comments

Only single-line `//` comments are supported. Block comments (`/* */`) are not part of the language.

```js
// This is a valid comment
auto x = 42; // inline comment
```

Block comments are rejected:

```js
/* This is not valid in JS-- */
```
