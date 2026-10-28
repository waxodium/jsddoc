# Array

Arrays in JSmm are used to store a sequential collection of values within a single variable. Depending on the keyword used during declaration, arrays can either store **multiple values of different data types** (heterogeneous) or be strictly constrained to a **single data type** (homogeneous).

## Array Types

### Dynamic Arrays (`auto`)
When declared with the `auto` keyword, an array acts as a flexible container capable of mixing multiple data types together.

```js
auto array_name = [0, "string", true, -79]
```

### Strongly-Typed Arrays
When declared with an explicit primitive type, the array enforces type safety. Data types other than `auto` require all elements to match the declared type. They behave identically to each other, with the strict exception of the `void` variable type, which cannot be used to initialize an array.

```js
bool array_bool = [true, false, false]
number array_num = [1, -0.12, 1e9]
string array_str = ["plattered_0", "A", "bob"]
bytes array_slot = [0x41, 0x7F, 0x00]

void array_void = [] // Error: void arrays are not allowed
```

## Changing Elements of an Array

You can access or modify a specific array element by referring to its index number. 

In JSmm, array indexes start at `0`. This means that `[0]` is the first element, `[1]` is the second element, and `[n-1]` is the last element.

```js
string slots = ["milk", "egg", "blueberry"]

// Modifying an element
slots[0] = "apple";

// Accessing an element
cat(slots[2]); // Outputs: blueberry
```

## Initializing Array Elements

JSmm supports different syntax structures for populating arrays at the time of declaration, depending on your allocation needs.

### Direct Literal Initialization
The standard method to populate an array is supplying a comma-separated list of elements inside square brackets `[]`. The compiler automatically calculates the array size based on the number of elements provided.

```js
number coefficients = [5.5, 10.2, -3.4]
```

### Designated Slot Initialization
You can initialize specific elements at distinct index positions during declaration. Any unassigned index positions automatically fall back to the default zero-value of the array's data type (`0` for number, `false` for bool, `""` for string).

```js
// Sets index 0 and 4. Indexes 1, 2, and 3 are automatically initialized to 0.
number sparse_scores = [0: 100, 4: 85]

// Accessing index 1 will returns "" as a no string.
string grades[3] = [0: "A+", 2: "C-"]

// Each and every index of this array cannot be changed including the entire variable itself.
const string grades[3] = [0: "A+", 2: "C-", 1: "B"]
```

### Empty Instantiation and Runtime Population
Arrays can be initialized completely empty and populated dynamically at runtime using explicit index assignments.

```js
string inventory = []

inventory[0] = "iron_ore"
inventory[1] = "coal"
```

