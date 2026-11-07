# JS-- Feature Status Registry

## COMPLETE Features

| Feature | Description | Evidence |
|---------|-------------|----------|
| i32<32, signed/unsigned> type specialization | Explicit integer types | parser.cc, checker.cc |
| type i32 = i32<32, signed> alias | Type alias pattern | parser.cc |
| f64 floating-point type | 64-bit floating-point | checker.cc |
| string and bytes types | Text and binary | lexer.cc, checker.cc |
| auto type inference | Inferred from initializers | parser.cc, checker.cc |
| bool and void types | Boolean and void | checker.cc |
| syscall() intrinsic | System calls | syscall.cc |
| All arithmetic operators | +, -, *, /, % | parser.cc, checker.cc |
| All comparison operators | ==, !=, <, >, <=, >= | parser.cc, checker.cc |
| Logical operators | &&, ||, ! | parser.cc, checker.cc |
| Control flow | if/else, while, for, break, continue | parser.cc |
| Pointers and arrays | Declaration, dereference | parser.cc |
| typeof() operator | Type inquiry | parser.cc, checker.cc |

## PARTIAL Features

| Feature | Description | Status |
|---------|-------------|--------|
| alloc/free memory management | alloc/free builtins exist | Codegen pending |
| memcpy/memset | Builtins declared | Codegen pending |
| closures | Not supported | MISSING |
| nested functions | Not supported | MISSING |
| generics | Not supported | MISSING |
| modules/imports | Not supported | MISSING |

## MISSING Features

| Feature | Description | Evidence |
|---------|-------------|----------|
| const keyword | Not in authorized set | Language spec |
| number keyword | Removed per spec | Language spec |
| const correctness | Not enforced | N/A |
| Enum type | Not implemented | N/A |
| Interface/traits | Not implemented | N/A |
| Generics/templates | Not implemented | N/A |
| Module system | Not implemented | N/A |
| Error types/exceptions | Not implemented | N/A |
| Recursion depth limit | Not specified | N/A |

## BUGGY Features

| Feature | Description | Evidence |
|---------|-------------|----------|
| ?? (nullish coalescing) | Present in lexer, parser rejects | parser.cc |
| ** (power) operator | Removed from grammar | parser.cc |

## UNRESOLVED Design Decisions

- Memory layout and alignment details
- Pointer size and representation
- Integer overflow behavior
- Floating-point precision model
- Struct field ordering and padding
- Exit code conventions
- Error reporting format
