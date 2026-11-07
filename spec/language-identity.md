# JS-- (JSMM) Language Identity

## Overview

JS-- (JSMM) is a statically-typed, natively-compiled subset of ECMAScript 2015 (ES2015) syntax. It restricts the full JavaScript language to a controlled subset suitable for system programming and native compilation without requiring a standard library. The language uses explicit type specialization via `i32<width, signed/unsigned>` syntax and removes the `number` keyword in favor of explicit type annotations.

## Design Characteristics

| Characteristic | Description |
|----------------|-------------|
| Base syntax | ES2015 (ECMAScript 2015) with restrictions |
| Compilation model | Ahead-of-time native compilation via LLVM |
| Execution model | Native execution without garbage collection |
| Memory management | Manual via `alloc()`/`free()` builtins |
| Type system | Static with type inference from initializers |
| Runtime facilities | Minimal -- syscall, cat, alloc, free, memcpy, memset |

## Core Concepts

- **Type specialization**: `i32<32, signed>` / `i32<32, unsigned>` for explicit integer types
- **Type aliases**: `type i32 = i32<32, signed>;` followed by `i32 x = 42;`
- **Authorized types**: `bool`, `i32<width, signed/unsigned>`, `f64`, `string`, `bytes`, `auto`, `void`
- **Removed keywords**: `number` (replaced by `i32`/`f64`), `const` (not in authorized set)
- **Function syntax**: `auto add(a, b) { return a + b; }` with `return` statements
- **System calls**: `syscall(num, args...)` intrinsic for OS interactions

## Compilation Model

```
Frontend: Lexer -> Parser -> AST -> Type Checker -> Codegen -> Executable
Target: x86_64 native code via LLVM
No garbage collection -- manual memory management via alloc()/free()
No runtime library -- only minimal builtins (syscall, cat, alloc, free, memcpy, memset)
```

## Implementation Status Summary

- **14/17 test files pass** with authorized syntax
- **8/17 test files fail** (legacy syntax explicitly removed per specification)
- Core compiler architecture (lexer, parser, AST, type checker, codegen) maintained
- All authorized features implemented per revised specification
