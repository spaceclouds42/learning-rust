# SpaceClouds42's notes form learning Rust


## Basic project management

### Creating a project

```bash
cargo new project_name
cd project_name
nano main.rs
```

### Compiling

```bash
cargo build
```

Executable is generated in the `target/debug/project_name` directory. When building for a release, use `cargo build --release` so that it compiles
with optimizations. Release executables are generated in the `target/release/project_name` directory. It will take longer to compile, but the 
executable will run faster than the unoptimized build.

To test that the code can compile without generating an executable, run `cargo check`.


### Running

To run a Rust program, simply run the executable generated by compiling. To compile and run at once, run `cargo run`.


## Basic syntax

### Importing

```rust
use std::io;
```

`use` will locally bind the path provided. To import multiple items from the same path, do `use a::b::{c, d, e::f};`. That would be the equivalent
of doing the following three use declarations:

```rust
use a::b::c;
use a::b::d;
use a::b::e::f;
```

### Functions

Functions are defined by `fn function_name() { ... }`. To call a function: `function_name();`.

Defining parameters: `fn do_something(x: i32, y: bool) { ... }`.

Defining return type: `fn returns_something() -> i32 { ... }`. The final expression in a function block is the return value, eg. `{ 5 }` returns 5.

Macros allow for different behavior for different parameters. To call a macro: `macro_name!();`. *The same as calling functions, plus an 
exclamation mark after the macro name.*

When passing in parameters to a function, it can be by reference or by value, and you can allow or disallow the method from mutating the variable.
Using `mut ` before the parameter allows the method to mutate it. Using `&` before a parameter will make it pass by reference, (you should probably
usually use this for complex types).


### Variables

```rust
let foo = bar;

let mut x = 2;
x = 3;
```

Creates a new variable `foo` and binds it to the value of the `bar` variable. Unless otherwise specified, variables are not mutable. Using the 
`mut` keyword makes it mutable.


### Associated Functions *(aka Static Methods)*

Functions that are implemented on a type, **rather than a particular instance of the type**, are called with the `Type::function()` syntax.


### Data Types

```rust
let foo: u32 = 100;
```

#### Scalar Types

Integers, floating-point numbers, Booleans, and characters

Integer types

| Length  | Signed | Unsigned |
|---------|--------|----------|
| 8 bit   | i8     | u8       |
| 16 bit  | i16    | u16      |
| 32 bit  | i32    | u32      |
| 64 bit  | i64    | u64      |
| 128 bit | i128   | u128     |
| arch    | isize  | usize    |

`isize` and `usize` use the computer architecture's size (32bit/64bit).

| Number literals | Example     |
|-----------------|-------------|
| Decimal         | 98_222      |
| Hex             | 0xff        |
| Octal           | 0o77        |
| Binary          | 0b1111_0000 |
| Byte (u8 only)  | b'A'        |

Floating-point types

```rust
let foo: f32 = 3.0;
```

Boolean type

```rust
let f: bool = false;
```

Character Type

```rust
let x: char = 'x';
```


#### Compound Types

Tuple type

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);

// Destructuring
let (x, y, z) = tup; // x = 500, y = 6.4, z = 1

// Accessing by index
let first = tup.0; // first = 500
```

Array type

```rust
let array: [i32; 5] = [1, 2, 3, 4, 5];

let a = [3; 5]; // a = [3, 3, 3, 3, 3]

// Accessing by index
let first = array[0]; // first = 1
```

### Control Flow

#### if

```rust
let number = 3;

if number < 5 {
	println!("true");
} else {
	println!("false");
}
```

Can be used in a `let` statement by returning the value in the arms.

```rust
let condition = true;
let number = if condition { 5 } else { 6 };
```

Both arms must return the same type!


#### Loops

```rust
// infinite loop (break and continue can be used)
loop {
	println!("infinity and beyond!");
}
```

`loop` blocks can return a value by adding a value after the `break` call. `let result = loop { break 10; };`, result = 10.

```rust
// conditional loop
while number != 0 {
	println!("number = {}", number);
	number -= 1;
}
```

```rust
// iterating
let a = [10, 20, 30, 40, 50];

for element in a.iter() {
	println!("val is {}", element);
}

for number in (1..4).rev() { // iterates through 1, 2, 3, but in reverse
	println!("{}!", number);
}
```
