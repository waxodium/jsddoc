# Constants
If the variables required to have a fixed value that
cannot be changed. Use `const` keyword

The `const` keyword declares a variable as constant,
which mean that is is unchangeable and read-only


```js
const PI = 3.14;
```

#### Table of Contents
- [Constant Types](#constant-types)
	- [Typed Constants](#typed-constants)
	- [AutoTyped Constants](#autotyped-constants)
	- [Constant Arrays](#constant-arrays)	

---

## Constant Types
Constant variable is the only dynamically typed
variable ever in JSmm programming language.

It supports all of every JSmm types which is divided
into two: Typed Constants and Autotyped Constants.

### Typed Constants
Typed Constants are declared with a defined type

```js
const string name = "Jane Doe";
```

### AutoTyped Constants
AutoTyped Constants are declared without a type, or with
the [`auto`](./types.md#auto) keyword.

```js
const auto a = true;
const b = "Alice Bobbison";

cat(a, b);
```

### Constant Arrays
More details in [array](./array.md)

```js
const items[3] = ["string", 14, true]
```

each and every index of the `items` array
cannot be redefine. 
