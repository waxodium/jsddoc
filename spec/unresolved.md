# JS-- Unresolved Design Decisions

## U.1 Integer Width Specification

- `i32<width, signed/unsigned>` syntax is supported
- Exact bit width semantics (8, 16, 32, 64) -- precise overflow behavior unspecified
- Signed vs unsigned comparison semantics

## U.2 Memory Model

- Pointer size (32-bit vs 64-bit)
- Alignment requirements for struct fields
- Byte ordering (endianness)
- Memory alignment constraints

## U.3 Runtime Behavior

- Exit code conventions
- Error reporting format
- Signal handling
- Standard I/O redirection

## U.4 Type System

- Exact promotion rules between i32/f64
- Implicit conversion policies
- Type alias resolution order
- Generic type parameters (if/when added)

## U.5 Future Feature Decisions

- Closure capture semantics (if added)
- Generic type parameter syntax
- Module import/export mechanism
- Error handling model (exceptions vs return codes)
