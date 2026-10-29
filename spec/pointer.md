# Pointers

Pointers provide direct access to memory addresses. They allow programs to reference existing values, modify memory, access byte sequences, and interact directly with operating-system resources.

JSmm supports typed pointers with static type checking. Its pointer system is designed for both ordinary programming and low-level system programming without requiring a standard library.

## Table of Contents

- [Pointer Declaration](#pointer-declaration)
- [Address-of Operator](#address-of-operator)
- [Dereferencing Pointers](#dereferencing-pointers)
- [Pointer Member Access](#pointer-member-access)
- [Pointer Assignment](#pointer-assignment)
- [Pointer Arithmetic](#pointer-arithmetic)
- [Byte Access](#byte-access)
- [Raw Memory Addresses](#raw-memory-addresses)
- [Null Pointers](#null-pointers)
- [Pointer Type Safety](#pointer-type-safety)
- [Memory Safety](#memory-safety)
- [Pointers and System Programming](#pointers-and-system-programming)

---

## Pointer Declaration

A pointer is a variable that stores a memory address.

### Syntax

```js
type* identifier = expression;
```

The type preceding `*` specifies the type of value referenced by the pointer.

### Example

```js
number value = 42;
number* ptr = &value;
```

In this example, `ptr` stores the address of `value`.

JSmm uses typed pointers to identify the type of value accessible through a pointer.

```js
number* num_ptr;
string* str_ptr;
bool* bool_ptr;
```

Each pointer type determines which operations are valid through that pointer.

A pointer can refer to an existing variable, an object, a byte in a byte sequence, or another valid memory location of a compatible type.

## Address-of Operator

The address-of operator `&` obtains the memory address of an addressable expression.

### Syntax

```js
&expression
```

### Example

```js
number age = 25;
number* ptr = &age;
```

The expression `&age` obtains the address of `age` and assigns it to `ptr`.

The pointer refers to the original variable rather than a copy of its value.

```js
number value = 10;
number* ptr = &value;

*ptr = 20;

cat(value); // Outputs: 20
```

Changing the value through the pointer changes the original variable.

The address-of operator can only be applied to expressions that represent addressable storage locations. Expressions that produce temporary values cannot be used when no addressable storage exists.

## Dereferencing Pointers

Dereferencing accesses the value stored at the memory address held by a pointer.

JSmm uses the `*` operator to dereference a pointer.

### Syntax

```js
*pointer
```

### Reading a Value

```js
number value = 42;
number* ptr = &value;

cat(*ptr); // Outputs: 42
```

The expression `*ptr` accesses the value referenced by `ptr`.

### Modifying a Value

```js
number value = 10;
number* ptr = &value;

*ptr = 50;

cat(value); // Outputs: 50
```

Dereferencing a pointer in an assignment modifies the referenced memory.

Dereferencing is valid only when the pointer refers to accessible memory containing a value of the expected type.

## Pointer Member Access

JSmm uses the member access operator `.` for both objects and pointers to objects.

Unlike C, JSmm does not require a separate `->` operator or explicit dereferencing to access an object's members through a pointer.

### Example

```js
Person person = Person();
Person* ptr = &person;

person.name = "Alice";
ptr.name = "Bob";

cat(person.name); // Outputs: Bob
```

When `ptr` points to an object, `ptr.name` accesses the object's `name` member directly.

The compiler determines whether member access operates on an object or through a pointer.

### Nested Member Access

The same syntax applies to nested objects.

```js
Person person = Person();
Person* ptr = &person;

ptr.address.city = "Singapore";
```

Member access follows the object structure without requiring explicit pointer dereferencing at every level.

Automatic pointer member access does not make invalid pointers safe. Accessing a member through a null, dangling, or otherwise invalid pointer is invalid.

## Pointer Assignment

Pointers can be assigned to other compatible pointers.

### Example

```js
number first = 10;
number second = 20;

number* ptr = &first;
ptr = &second;
```

After the assignment, `ptr` points to `second` instead of `first`.

Changing the pointer's target does not modify either variable's value.

```js
*ptr = 30;

cat(first);  // Outputs: 10
cat(second); // Outputs: 30
```

Pointer assignment changes the stored address. Dereferencing and assigning through a pointer changes the referenced value.

Pointers of incompatible types cannot be assigned to one another without an explicit conversion supported by the language.

## Pointer Arithmetic

Pointer arithmetic allows a program to move through consecutive memory locations.

This capability is useful when working with byte sequences, memory buffers, operating-system interfaces, and data structures stored in contiguous memory.

### Syntax

```js
pointer + offset
pointer - offset
pointer1 - pointer2
```

The exact operations permitted depend on the pointer type.

For byte pointers, adding or subtracting an integer offset moves the pointer by that number of bytes.

### Example

```js
byte* ptr = /* address of a byte */;
byte* next = ptr + 1;
```

Here, `next` points to the byte immediately following the byte referenced by `ptr`.

Pointer arithmetic does not allocate memory, extend a buffer, or validate the destination address.

A pointer must not be dereferenced unless it points to accessible memory. Programs must also avoid arithmetic that produces an invalid address or moves outside the permitted memory region.

Subtracting two pointers is only valid when both pointers refer to the same memory region and the result is representable.

## Byte Access

Byte access allows programs to inspect and modify individual bytes in memory.

JSmm uses `bytes` to represent dynamically sized sequences of raw bytes. A byte sequence can contain text, binary data, file contents, network packets, or manually constructed data structures.

Byte access is separate from `string`. Strings are intended for high-level text operations and are not the interface for explicit memory manipulation.

### Accessing a Byte Sequence

```js
bytes data = [0x48, 0x65, 0x6C, 0x6C, 0x6F];
```

The sequence contains five bytes.

A program must be able to obtain the address of its first byte and the number of bytes it contains.

### Accessing Individual Bytes

```js
byte first = data[0];
data[0] = 0x41;
```

The first statement reads the first byte. The second modifies it.

The byte type represents a single unsigned eight-bit value in the range `0` through `255`.

### Obtaining a Byte Pointer

```js
byte* ptr = &data[0];
```

The pointer refers to the first byte of the sequence.

Pointer arithmetic can then be used to access subsequent bytes, provided the resulting address remains within the accessible memory region.

### Byte Sequence Length

Programs must be able to obtain the number of bytes in a sequence without relying on a standard library.

The byte length describes the sequence's actual size, not the number of characters that its contents might represent.

For example, a sequence containing five bytes has a byte length of five, regardless of whether those bytes encode text or binary data.

The syntax for retrieving the length is defined by the language's byte-sequence operations.

## Raw Memory Addresses

Raw memory addresses allow programs to work with memory whose address is obtained externally, including addresses returned by operating-system calls.

A pointer created with the address-of operator refers to an existing addressable value. System programming also requires a defined way to convert an externally obtained address into a pointer.

### Converting an Address

The language must provide an explicit conversion from a valid numeric address to a pointer.

Conceptually:

```js
number address = /* an address obtained from the operating system */;
byte* ptr = /* explicitly convert address to byte* */;
```

The conversion syntax must be defined by JSmm's type and conversion rules.

A numeric address does not automatically guarantee that memory exists at that location. The resulting pointer is valid only when the address refers to accessible memory with the required permissions and lifetime.

Converting an arbitrary number to a pointer does not allocate memory or make an invalid address safe.

### Accessing Raw Memory

Raw pointers allow programs to access memory directly without requiring an object or variable declaration for every memory location.

This capability can be used to work with memory-mapped regions, operating-system interfaces, and buffers obtained through system calls.

The program is responsible for ensuring that the address, access size, alignment, and memory permissions are valid.

## Null Pointers

A null pointer does not refer to a valid object or value.

JSmm uses `null` to represent a null pointer.

### Example

```js
number* ptr = null;
```

A null pointer must not be dereferenced or used for member access.

```js
number* ptr = null;

// Invalid: ptr does not reference a valid value.
cat(*ptr);
```

Programs must ensure that a pointer refers to valid memory before accessing its target.

A null pointer is distinct from a pointer whose address is zero only if the language or target platform defines such a distinction. JSmm must define how null pointers are represented by each supported target.

## Pointer Type Safety

JSmm checks pointer types during compilation.

A pointer must reference a compatible type.

### Example

```js
number value = 42;
number* ptr = &value;
```

Assigning an incompatible pointer type is rejected unless an explicit conversion is supported.

```js
number value = 42;
number* ptr = &value;

// Type error: incompatible pointer types.
string* text_ptr = ptr;
```

Pointer type checking prevents certain incompatible operations. It cannot guarantee that every pointer refers to valid memory.

Explicit conversions and raw memory access may bypass some of the protections provided by ordinary type checking.

## Memory Safety

Raw pointers provide direct memory access but can introduce memory errors.

Examples include:

- Dereferencing null pointers.
- Accessing memory after its lifetime has ended.
- Accessing invalid memory addresses.
- Reading or writing beyond a buffer's bounds.
- Using a pointer after its target has been deallocated.
- Performing invalid pointer arithmetic.
- Accessing memory with an incompatible type or alignment.

JSmm's static type checking can detect certain invalid operations, but raw pointers retain the risks associated with low-level memory access.

Programs using raw pointers must ensure that memory remains valid for the duration of every access.

## Pointers and System Programming

Pointers provide the foundation for interacting directly with operating-system services without requiring a standard library.

System calls generally receive numeric arguments and memory addresses. They do not operate on high-level JSmm strings or understand the meaning of the data at a given address.

### Example: Writing Bytes

Conceptually, a program can pass a byte pointer and a byte count to a system call:

```js
bytes message = [0x48, 0x65, 0x6C, 0x6C, 0x6F, 0x0A];

byte* ptr = &message[0];
number size = 6;

// Pass ptr and size to the operating system.
```

The pointer identifies the first byte. The size specifies how many bytes the operation may read.

The operating system does not need to know whether the bytes represent text or binary data.

A system call may process fewer bytes than requested or return an error. Programs must handle the returned result and must not assume that every operation completes in full.

### Responsibilities of the Compiler

The compiler must define consistent rules for:

- Pointer representation and alignment.
- Address-of and dereferencing operations.
- Pointer arithmetic.
- Byte access and byte sequence lengths.
- Explicit conversions between numeric addresses and pointers.
- Null pointer representation.
- Pointer argument passing to system calls.

These rules must agree with the memory model and calling conventions of each supported target.


