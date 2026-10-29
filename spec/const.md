# Constants

Use the `const` keyword to declare a variable with a fixed value that cannot be changed. Constants are read-only and unchangeable.

```js
const PI = 3.14;

```

#### Table of Contents

* [Constant Types](#constant-types)
* [Typed Constants](#typed-constants)
    * [Union Declarations](#union-declarations)
* [AutoTyped Constants](#autotyped-constants)
* [Constant Arrays](#constant-arrays)



---

## Constant Types

Constants are the only dynamically typed variables in the JSmm programming language. 
They support all JSmm types, divided into two categories: Typed Constants and AutoTyped Constants.

### Typed Constants

Typed constants are declared with an explicit type.

```js
const string name = "Jane Doe";
```

#### Union Declarations

Unlike regular variables, constants cannot use union types with multiple types because their value cannot be redefined.

For more details, see [Types](./types.md#union-types-with-variables).

```js
const string, number = "hello"; // rejected: const cannot be redefined
```

### AutoTyped Constants

AutoTyped constants are declared without an explicit type or with the 
[`auto`](./types#auto) keyword. 
Declaring them without `auto` behaves the exact same way.

```js
const auto a = true;
const b = "Alice Bobbison";

cat(a, b);

```

### Constant Arrays

For more details, see [Array](./array.md).

```js
const items[3] = ["string", 14, true];
```

Each and every index of the `items` array cannot be redefined.

