# Types

JSmm provides a minimal type system designed to keep declarations intuitive while enforcing predictable compilation behavior.

#### Table of Contents
- [Built-in Types](#built-in-types)
  - [auto](#auto)
  - [string](#string)
  - [number](#number)
  - [bool](#bool)
  - [void](#void)
  - [bytes](#bytes)
  - [array](#array)
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

List of primitive and core composite types supported in the JSmm programming language:

### `auto`
Infers a value's type at compile time, reducing the need for explicit type annotations while preserving static type checking.
- **Syntax:** `auto <identifier> = <expression>;`
- **Example:** `auto value = 42;`

### `string`
Represents text and provides a dedicated type for working with textual data.
- **Syntax:** `string <identifier> = "<value>";`
- **Example:** `string message = "hello";`

### `number`
Represents numeric values, including integers and floating-point numbers, through a unified numeric type.
- **Syntax:** `number <identifier> = <numeric_literal>;`
- **Example:** `number ratio = 3.14;`

### `bool`
Represents Boolean truth values, either `true` or `false`.
- **Syntax:** `bool <identifier> = <boolean_literal>;`
- **Example:** `bool isReady = true;`

### `void`
Indicates that a function does not return a value.
- **Syntax:** `void <identifier>(<parameters>) { ... }`
- **Example:** `void clear() {}`

### `bytes`
Represents a dynamically sized sequence of raw bytes, designed for efficient binary data processing.
- **Syntax:** `bytes <identifier> = [<hex_or_integer_literals>];`
- **Example:** `bytes stream = [0x00, 0xFF];`

### `array`
Represents a dynamically sized collection that can contain values of different types. Mixed arrays provide flexibility for heterogeneous data, with potential performance overhead compared to homogeneous arrays.
- **Syntax:** `array <identifier> = [<elements>];`
- **Example:** `array items = [1, "two", false];`

---

## Union Types

Union types allow a variable, parameter, or function return value to represent more than one type. In JSmm, union types are declared by separating multiple types with a comma (`,`).

This allows functions to accept different kinds of values while preserving static type checking.

#### Syntax

```js
type1, type2 functionName(parameters) {
    // function body
}
```

The declared types represent the possible types of the function's return value.

#### Example

```js
string, number add(auto a) {
    if (typeof a == number) {
        return a + 1; // returns number
    }
    return a; // returns string
}
```

In this example, `add` accepts a parameter of type `auto` and can return either a `number` or a `string`.
- If `a` is a number, the function returns `a + 1`.
- Otherwise, it returns `a` as a string, assuming the input is a string.

The return type signature `string, number` explicitly declares both possible output paths.

### Union Type Checking

JSmm verifies that a function's return statements are structurally compatible with its declared return types.

```js
string, number getValue(bool condition) {
    if (condition) {
        return 42;
    }
    return "hello";
}
```

Both return statements are valid because the function lists `number` and `string` as permissible return targets. Conversely, returning a type outside the declared union triggers a compile-time type error:

```js
string, number getValue() {
    return true; // Type error: bool is not allowed
}
```

### Union Types with Variables

Union types are also valid when a single variable needs to hold different payload types throughout execution.

```js
string, number value = 10;
value = "hello";
```

Here, `value` can safely alternate between holding a number and a string.

#### Union Types vs `auto`

The `auto` type infers a concrete, single type at compile time from its initializer, whereas a union type explicitly allows multiple dynamic assignments.

```js
auto count = 10;
string, number value = 10;
```

In this setup:
- `count` has its type inferred strictly as `number`.
- `value` is explicitly opened to accept either a `string` or a `number`.

> Use `auto` for strict single-type inference from an initializer. Use a union declaration when a variable must accept assignments from multiple distinct types.

---

## Type Compatibility

Type compatibility determines whether a value can be cleanly assigned to a variable, passed as a function argument, or returned from an active routine. JSmm checks these relationships during compilation.

### Assignment Compatibility

A value can be assigned to a variable only when its underlying type matches or satisfies the target variable's type constraints.

```js
number age = 25;
string name = "Alex";
bool active = true;
```

The following initialization illustrates an incompatible assignment variant:

```js
number age = "twenty-five"; // Type error
```

A `string` literal cannot be bound to a variable declared as `number` unless a primitive type cast or explicit coercion option is used.

### Parameter Compatibility

Arguments passed into a function must conform to their corresponding parameter declarations.

```js
number square(number n) {
    return n * n;
}

number result = square(5);
```

Passing an argument out of bounds results in an upfront compiler rejection:

```js
number result = square("five"); // Type error
```

### Return Type Compatibility

A function's execution branches must yield values that align with its declared return signature.

```js
number getCount() {
    return 10;
}

void printCount() {
    // Performs an operation without returning a value
}
```

---

## Type Inference

Type inference allows JSmm to determine an assignment's concrete type implicitly, eliminating boilerplate annotations without compromising the integrity of static type checks.

```js
auto name = "Alice";
auto age = 25;
auto isActive = true;
```

The engine evaluates the code and derives the following map:

| Declaration | Inferred Type |
| :--- | :--- |
| name | `string` |
| age | `number` |
| isActive | `bool` |

### Inference Limitations

Type inference relies on explicit initialization paths. If an expression leaves the expected layout ambiguous, an explicit type signature must be provided.

```js
auto value = 10; // Explicitly initialized: infers number safely.
```

---

## Type Errors

Type errors occur when an operational expression breaks the structural typing policies of JSmm. These errors are caught at compile time to block corrupted payloads from reaching runtime execution.

### Incompatible Assignment
```js
number count = "hello";
```

### Invalid Operation
```js
number result = 10 + "hello";
```

### Invalid Return Type
```js
number getValue() {
    return "hello";
}
```

### Invalid Argument
```js
number double(number value) {
    return value * 2;
}

double(true);
```

