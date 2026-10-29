# Types

#### Table of Contents

- [Built-in Types](#built-in-types)
  - [`auto`](#auto)
  - [`string`](#string)
  - [`number`](#number)
  - [`bool`](#bool)
  - [`void`](#void)
  - [`bytes`](#bytes)
- [Type Aliases](#type-aliases)
  - [Declaration Syntax](#declaration-syntax)
  - [Examples](#examples)
- [Union Types](#union-types)
  - [Union Type Checking](#union-type-checking)
  - [Union Types with Variables](#union-types-with-variables)
  - [Union Types vs `auto`](#union-types-vs-auto)
- [Type Compatibility](#type-compatibility)
  - [Assignment Compatibility](#assignment-compatibility)
  - [Parameter Compatibility](#parameter-compatibility)
  - [Return Type Compatibility](#return-type-compatibility)
- [Type Inference](#type-inference)
  - [Inference Limitations](#inference-limitations)
- [Type Errors](#type-errors)
  - [Incompatible Assignment](#incompatible-assignment)
  - [Invalid Operation](#invalid-operation)
  - [Invalid Return Type](#invalid-return-type)
  - [Invalid Argument](#invalid-argument)

---

## Built-in Types

JSmm provides built-in types for common values and operations.

### `auto`

Infers a value's type at compile time, reducing the need for explicit type annotations while preserving static type checking.

- **Syntax:** `auto <identifier> = <expression>;`
- **Example:**

```js
auto value = 42;
```

### `string`

Represents text and provides a dedicated type for working with textual data.

- **Syntax:** `string <identifier> = "<value>";`
- **Example:**

```js
string message = "hello";
```

### `number`

Represents numeric values, including integers and floating-point numbers, through a unified numeric type.

- **Syntax:** `number <identifier> = <numeric_literal>;`
- **Example:**

```js
number ratio = 3.14;
number count = 42;
```

### `bool`

Represents Boolean truth values: `true` and `false`.

- **Syntax:** `bool <identifier> = <boolean_literal>;`
- **Example:**

```js
bool isReady = true;
```

### `void`

Indicates that a function does not return a value.

- **Syntax:** `void <identifier>(<parameters>) { ... }`
- **Example:**

```js
void clear() {}
```

### `bytes`

Represents a dynamically sized sequence of raw bytes, intended for binary data.

- **Syntax:** `bytes <identifier> = [<byte_literals>];`
- **Example:**

```js
bytes stream = [0x00, 0xFF];
```

`bytes` is intended for raw binary data, whereas `string` represents text. Their operations and memory semantics are separate.

---

## Type Aliases

A type alias introduces a reusable name for a type expression. JSmm uses the `type` keyword to declare aliases.

Aliases allow developers to give meaningful names to existing types and define reusable types without introducing a separate built-in keyword for every type variation.

### Declaration Syntax

```js
type <name> = <type_expression>;
```

- `type` is the declaration keyword.
- `<name>` is the alias being defined.
- `<type_expression>` specifies the underlying type.

The `type` keyword is used in declarations. It is not itself a type, and it does not create a runtime value.

### Examples

An alias can provide a more descriptive name for an existing type.

```js
type identifier = number;
type message = string;

identifier value = 42;
message text = "hello";
```

Here, `identifier` refers to `number`, while `message` refers to `string`.

Aliases can also name custom integer types:

```js
type byte = int(1, unsigned);
type registers_3bytes = int(3, unsigned);
```

These examples use the built-in `int()` function to specify integer storage size in bytes and signedness. The aliases provide reusable names for those type expressions.

### Naming Rules

Type alias names follow JSmm's identifier naming rules.

The `type` keyword is reserved for type alias declarations and cannot be used as an ordinary identifier.

The language must define whether aliases can reference declarations that appear later in the source and how duplicate or cyclic alias declarations are diagnosed.

---

## Union Types

Union types allow a variable, parameter, or function return value to represent more than one type.

In JSmm, union types are declared by separating multiple types with a comma.

### Syntax

```js
type1, type2 functionName(parameters) {
    // Function body
}
```

The declared types represent the possible return types of the function.

### Example

```js
string, number add(auto a) {
    if (typeof a == number) {
        return a + 1;
    }

    return a;
}
```

In this example, `add` declares that it can return either a `string` or a `number`.

- If `a` is a number, the function returns `a + 1`.
- Otherwise, the function returns `a`, provided that the value is a string.

The return signature `string, number` declares the permitted return types.

### Union Type Checking

JSmm checks whether return statements are compatible with the function's declared return types.

```js
string, number getValue(bool condition) {
    if (condition) {
        return 42;
    }

    return "hello";
}
```

Both return statements use types declared in the return signature.

Returning an undeclared type is invalid:

```js
string, number getValue() {
    return true; // Type error: bool is not allowed
}
```

### Union Types with Variables

A union declaration can allow a variable to hold values of different permitted types.

```js
string, number value = 10;
value = "hello";
```

The declared union allows `value` to hold either a string or a number, subject to the language's assignment and type-checking rules.

A `const` declaration makes a variable read-only after initialization. It does not mean that the variable can be redeclared.

### Union Types vs `auto`

`auto` infers a single type from an initializer, whereas a union explicitly declares multiple permitted types.

```js
auto count = 10;
string, number value = 10;
```

- `count` infers its type from the initializer as `number`.
- `value` explicitly permits `string` and `number`.

Use `auto` when a single inferred type is sufficient. Use a union when multiple types must be permitted by the declaration.

---

## Type Compatibility

Type compatibility determines whether a value can be assigned to a variable, passed to a function, or returned from a function. JSmm checks these relationships during compilation.

### Assignment Compatibility

A value can be assigned to a variable when its type satisfies the target type's compatibility rules.

```js
number age = 25;
string name = "Alex";
bool active = true;
```

An incompatible assignment produces a type error:

```js
number age = "twenty-five"; // Type error
```

Conversions between types are governed by JSmm's conversion rules.

### Parameter Compatibility

Arguments passed to a function must be compatible with their corresponding parameter types.

```js
number square(number n) {
    return n * n;
}

number result = square(5);
```

Passing an incompatible argument is invalid:

```js
number result = square("five"); // Type error
```

### Return Type Compatibility

A function's return statements must conform to its declared return type.

```js
number getCount() {
    return 10;
}

void clear() {
    // Performs an operation without returning a value.
}
```

---

## Type Inference

Type inference allows JSmm to determine a variable's type from its initializer, reducing the need for explicit annotations while preserving static type checking.

```js
auto name = "Alice";
auto age = 25;
auto isActive = true;
```

The inferred types are:

| Declaration | Inferred type |
|---|---|
| `name` | `string` |
| `age` | `number` |
| `isActive` | `bool` |

### Inference Limitations

Type inference depends on the information available to the compiler. When a type cannot be determined unambiguously, an explicit type declaration may be required.

```js
auto value = 10;
```

Here, the initializer provides enough information to infer `number`.

The language specification must define inference behavior for expressions involving unions, aliases, and function calls.

---

## Type Errors

Type errors occur when a declaration, assignment, operation, argument, or return value violates JSmm's type rules.

### Incompatible Assignment

```js
number count = "hello";
```

The string value is incompatible with the declared numeric type.

### Invalid Operation

```js
number result = 10 + "hello";
```

The operands are incompatible under the numeric addition rules.

### Invalid Return Type

```js
number getValue() {
    return "hello";
}
```

The function declares `number` but returns a string.

### Invalid Argument

```js
number double(number value) {
    return value * 2;
}

double(true);
```

The argument is a Boolean value, but the function expects a number.

### Invalid Type Alias

A type alias must refer to a valid type expression.

```js
type invalid = unknown_type;
```

If `unknown_type` is not a declared or built-in type, the compiler should report an invalid type reference.


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
