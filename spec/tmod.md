# Type Modifiers

Type modifiers specify additional properties of a type, such as whether an integer can represent negative values. In JSMM, `signed` and `unsigned` specify the signedness of integer types.

## Signedness Modifiers

### `signed`

The `signed` modifier specifies an integer type that can represent both negative and non-negative values.

**Example:**

```js
type temperature = int(2, signed);
type file_offset = int(8, signed);

temperature value = -10;
```

The integer's storage size determines its representable range according to JSMM's integer representation rules.

### `unsigned`

The `unsigned` modifier specifies an integer type that represents non-negative values.

**Example:**

```js
type byte = int(1, unsigned);
type permissions = int(4, unsigned);

byte value = 255;
```

Unsigned integers are useful for values that do not require negative numbers, including bit fields, flags, and binary data.

## Syntax

Signedness is specified as part of an integer type expression.

```js
int(<size>, signed)
int(<size>, unsigned)
```

- `<size>` specifies the integer's storage size in bytes.
- `signed` specifies a signed integer representation.
- `unsigned` specifies an unsigned integer representation.

These are type-specification forms, not runtime function calls.

## Using Modifiers with Type Aliases

The `type` keyword allows developers to define reusable names for integer types.

```js
type signed_integer = int(4, signed);
type unsigned_integer = int(4, unsigned);

signed_integer temperature = -20;
unsigned_integer counter = 100;
```

The aliases can then be reused in variable declarations without repeating the integer type expression.

## Type Rules

JSMM's language specification must define:

- Which storage sizes are supported.
- The integer representation and value range for each signedness.
- Overflow and underflow behavior.
- Whether conversions between signed and unsigned types are implicit or require explicit conversion.
- How arithmetic and comparisons behave when operands have different signedness.

## Declaration Qualifiers

`const` is a declaration qualifier rather than an integer signedness modifier. It indicates that a declared variable cannot be reassigned after initialization.

```js
const number limit = 100;
```

The `const` qualifier and integer signedness serve different purposes: `const` restricts reassignment, while `signed` and `unsigned` describe integer representation.
