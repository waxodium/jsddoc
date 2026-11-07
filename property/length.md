# The `.length` Property

`.length` reports the size of a value. It is a read-only property, not a method.

```js
string text = "hello";
auto size = text.length;
```

Use `value.length`, not `value.length()`.

## Meaning by type

| Type | `.length` means | Example |
|---|---|---|
| `string` | UTF-8 byte length, not character count | `"hello".length == 5` |
| `bytes` | Byte count | `(bytes "AB").length == 2` |

For strings, non-ASCII characters can use more than one byte:

```js
"\u{1F600}".length == 4
```

## Read-only

Assigning to `.length` is a compile-time error:

```js
string s = "hello";
s.length = 5;
```

```
jsmm: invalid assignment target: length
```

Updating it is also rejected:

```js
s.length++;
```

```
jsmm: invalid assignment target: length
```
