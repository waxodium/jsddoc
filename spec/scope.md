# JS-- Scope and Name Resolution

## Scopes

1. **Global scope**: File-level declarations
2. **Function scope**: Function parameters and local variables
3. **Block scope**: Variables within `{}` blocks
4. **Type scope**: `type` declarations have file scope

## Name Resolution

- Names are resolved in innermost scope first
- Type aliases resolve to their specialized type
- Function parameters shadow outer scope variables
- `auto` variables infer type from initializer

## Variable Declaration Rules

```js
auto x = 42;          // Valid -- inferred from initializer
i32 x = 42;           // Valid -- explicit type
f64 x = 3.14;         // Valid -- explicit type
string s = "hello";   // Valid -- explicit type
bytes d = "content";  // Valid -- explicit type
bool b = true;        // Valid -- explicit type
```

## Variable Shadowing

Inner scope variables shadow outer scope variables. Type aliases do not create new scopes.
