# Variables

A variable is a named storage location that holds a value during program execution.

In JSmm, variables are governed by their declared or inferred [type](./types.md). The type determines which values can be assigned to a variable and how those values can be used.

## Table of Contents

- [Variable Declaration](#variable-declaration)
- [Variable Initialization](#variable-initialization)
- [Variable Types](#variable-types)
- [Variable Assignment](#variable-assignment)
- [Type Safety](#type-safety)

---

## Variable Declaration

A variable declaration introduces a named variable into the program.

### Syntax

```js
type identifier = expression;
```

### Example

```js
number age = 25;
string name = "Alice";
bool isActive = true;
```

Each declaration specifies a variable's type, name, and initial value.

## Variable Initialization

Initialization assigns the initial value to a variable when it is declared.

```js
number count = 10;
string message = "Hello";
bool enabled = false;
```

JSmm checks whether the initial value is compatible with the declared type during compilation.

## Variable Types

Variables can use JSmm's supported [built-in types](./types.md#built-in-types), including `number`, `string`, `bool`, `bytes`, and `array`.

```js
number score = 100;
string username = "guest";
bool authenticated = false;
bytes data = [0x01, 0x02];
array items = [1, "two", false];
```

Variables can also use `auto` to infer their types from their initial values.

```js
auto count = 10;
auto title = "JSmm";
auto ready = true;
```

The inferred types are `number`, `string`, and `bool`, respectively.

For details about supported types and type inference, see [Types](./types.md).

## Variable Assignment

An existing variable can receive a new value through assignment, provided the value satisfies the variable's type constraints.

```js
number count = 10;
count = 20;
```

Variables declared with a single concrete type cannot be assigned values of incompatible types.

```js
number count = 10;
count = "hello"; // Type error
```

For variables that need to accept values of different types, JSmm supports [union types](./types.md#union-types).

```js
string, number value = 10;
value = "hello";
```

## Type Safety

JSmm checks variable declarations, initialization, and assignments at compile time.

Incompatible values cause compilation errors rather than being silently accepted.

```js
number age = "twenty"; // Type error
bool active = 1;       // Type error
```
