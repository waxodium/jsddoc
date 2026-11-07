# jsddoc
Official repository for JS-- (JSMM) programming language test cases, documentations and guides for the entire language.

Compiler source code if you're looking for it:
[jsmm](https://github.com/waxodium/jsmm)

![License: MIT](./assets/license-mit.svg)

## Preface
Check the Installation steps from [jsmm homepage](https://github.com/waxodium/jsmm#home).
Make sure your machines have met all of the requirements for the installation.

Language stage is still in Bootstrapping phase.
Currently written in C++ using `LLVM library` and `glibc 2.44` all relying on `GNU C compiler 16.2.1`

The project major goal is to finish host implementation and Compiler Primitives.

## Getting Started
Read the [contributing guide](./CONTRIBUTING.md) of JSMM for jsddoc and jsmm

**Note**: This repository only contains the documented language and concepts.
Please note that the code is kept in a separate repository.

#### Language specifications tutorial
Detailed friendly tutorials and usage for JS-- programming language.
- [JS-- Language Identity](./spec/language-identity.md)
- [JS-- Lexical Specification](./spec/lexical.md)
- [JS-- Formal Grammar](./spec/grammar.md)
- [JS-- Type System](./spec/type-system.md)
- [JS-- Language Semantics](./spec/semantics.md)
- [JS-- Scope and Name Resolution](./spec/scope.md)
- [JS-- Advanced Features](./spec/advanced.md)
- [JS-- Builtins and Standard Library](./spec/builtins.md)
- [JS-- Feature Status Registry](./spec/feature-status.md)
- [JS-- Conformance Tests](./spec/conformance-tests.md)
- [JS-- Known Bugs and Limitations](./spec/bugs-limitations.md)
- [JS-- Unresolved Design Decisions](./spec/unresolved.md)

#### Built-in Functions
- [cat()](./builtin/cat.md)
- [syscall()](./builtin/syscall.md)
- [alloc()](./builtin/alloc.md)
- [free()](./builtin/free.md)
- [memcpy()](./builtin/memcpy.md)
- [memset()](./builtin/memset.md)

#### Built-in Properties
- [.length](./property/length.md)

#### Language spec with EBNF
- [EBNF Grammar](./spec/grammar.md)

## Joining
Source code is all opensource, free of charge for usage and changes.

In need for kind developers who would voluntarily contribute to the code and language until the turning point happen.

You can contribute to the jsddoc and the actual JS-- compiler repository.

For jsddoc, it is based on documentations and test suites.
Anyone can make an issue for a feature request, redesign, and make language architectural decisions.
