# JS-- Formal Grammar

EBNF-style grammar reflecting the actual language syntax.

## Program

```
program -> statement*
```

## Statements

```
statement -> function_declaration
statement -> type_declaration
statement -> variable_declaration
statement -> return_statement
statement -> if_statement
statement -> while_statement
statement -> for_statement
statement -> break_statement
statement -> continue_statement
statement -> empty_statement
statement -> block
statement -> expression_statement
```

## Function Declarations

```
function_declaration -> "auto" IDENTIFIER "(" params ")" block
params -> identifier ("," identifier)*
```

## Type Declarations

```
type_declaration -> "type" IDENTIFIER "=" type_spec ";"
type_spec -> i32_type | f64_type | string_type | bytes_type
i32_type -> "i32"("<" number("," "signed" | "unsigned")?">") | "i32"
```

## Variable Declarations

```
variable_declaration -> type_name IDENTIFIER ("=" initializer)? ";"
initializer -> expression
type_name -> i32_specifier | f64_type | string_type | bytes_type | "auto" | "bool" | "void"
i32_specifier -> "i32"("<" number("," "signed" | "unsigned")?">") | "i32"
```

## Expressions

```
expression -> assignment_expression
assignment_expression -> conditional_expression
conditional_expression -> logical_or_expression
logical_or_expression -> logical_and_expression ("||" logical_and_expression)*
logical_and_expression -> inclusive_or_expression ("&&" inclusive_or_expression)*
inclusive_or_expression -> exclusive_or_expression ("|" exclusive_or_expression)*
exclusive_or_expression -> and_expression ("^" and_expression)*
and_expression -> equality_expression ("&" equality_expression)*
equality_expression -> relational_expression ("==" | "!=" relational_expression)*
relational_expression -> shift_expression ("<" | ">" | "<=" | ">=" shift_expression)*
shift_expression -> additive_expression ("<<" | ">>" additive_expression)*
additive_expression -> multiplicative_expression ("+" | "-" multiplicative_expression)*
multiplicative_expression -> primary ("*" "/" "%" primary)*
primary -> "(" expression ")"
        | "!" expression
        | "-" primary
        | "+" primary
        | number_literal
        | string_literal
        | bool_literal
        | null_literal
        | "sizeof" "(" type ")"
        | "alignof" "(" type ")"
        | "offsetof" "(" IDENTIFIER "," IDENTIFIER ")"
        | "alloc" "(" expression ")"
        | "free" "(" expression ")"
        | "memcpy" "(" expression "," expression "," expression ")"
        | "memset" "(" expression "," expression "," expression ")"
        | identifier
        | array_literal
```

## Type Expressions

```
type_expr -> type_name ("[" number "]")?
type_name -> "i32" | "f64" | "string" | "bytes" | "bool" | "auto" | "void" | IDENTIFIER
i32_type -> "i32"("<" number("," "signed" | "unsigned")?">") | "i32"
```

## Function Parameters

```
params -> IDENTIFIER ("," IDENTIFIER)*
```

## Block

```
block -> "{" statement* "}"
```

## Literals

```
number_literal -> [/-/]?[0-9]+
string_literal -> '"' [^"]* '"'
bool_literal -> "true" | "false"
null_literal -> "null"
```
