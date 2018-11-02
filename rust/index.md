# Rust Journey

[Rust](https://www.rust-lang.org) A systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.

## New project

```rust
cargo new foobar
```

## Comments

```rust
// A comment here

let hello = "hello"; // Inline comment
```

## Data types

* Four primary scalar types: integers, floating-point numbers, booleans, and characters

### Integer types

* Signed integers are positive or negative numbers
* Unsigned are only positive numbers

| Length  | Signed | Unsigned |
|---------|--------|----------|
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

### Floating-point types

* Floating-point numbers are represented according to the IEEE-754 standard
* The `f32` type is a single-precision float, and `f64` has double precision

```rust
    let x = 2.0; // f64
    let y: f32 = 3.0; // f32
```

### Boolean types

* `true` or `false`
* The Boolean type in Rust is specified using `bool`

```rust
let t = true;

// With explicit type annotation
let likely_false: bool = false;
```

### Character types

* Characters are specified with a single `'`
* Can represent a lot more than just ASCII

```rust
  let c = 'z';
  let heart_eyed_cat = '😻';
```

## Variables

* Variables by default, are immutable (i.e. not subject to change)

```rust
  let x = 5;
  x = 6; // Returns an error

  let mut x = 5;
  x = 6; // No error
```

## String concatenation

```rust
let hello = "hello";
let world = "world";

println!("{} {}", hello, world);
```

## Strings and characters

```rust
// This is a string with length of 1
"a"

// This is a string with length of 3
"abc"

// This is a single character
'a'

// An empty string
""

// Error: Must contain 1 character
'abc'

// Error: Must contain 1 character
''
```

## Conditions

```rust
let is_one = 1 == 1;

println!("{}", is_one); // true
```

## Tuples

* Grouping together some number of other values with a variety of types

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);

// Or
let tup = (500, 6.4, 1);
let (x, y, z) = tup;

println!("{}", tup.0) // Returns 500
```

## Arrays

* Collection of similar types

```rust
let months: [&str; 12] = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
println!("{}", a[1]); // February
```

## Structs

* Collection of different types

```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {
    let mut user1 = User {
        email: String::from("user1@example.com"),
        username: String::from("user1"),
        active: true,
        sign_in_count: 1,
    };

    user1.email = String::from("user111@example.com");

    let mut user2 = User {
        email: String::from("user2@example.com"),
        username: String::from("user2"),
        ..user1 // The syntax .. specifies that the remaining fields (from user1) be explicitly set on user2
    };

    println!("{:?}", user2);
}
```

## Tuple structs

* Like structs, but don’t have names associated with their fields
* They just have the types of the fields

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);
```

## Functions

```rust
fn main() {
    println!("Hello, world!");

    println!("{}", add_one(5));
}

// Type annotated
// Expects a 32 bit unsigned (negative or positive number)
// Returns a 32 bit unsigned integer
fn add_one(x: u32) -> u32 {
    x + 1
}
```

## Methods

* Methods are similar to functions
* They are declared with the `fn`
* They can have parameters and a return value
* The difference: They are defined within the context of a struct (or an enum or a trait object)
* The benefit of using methods instead of functions, in addition to using method syntax and not having to repeat the type of self in every method's signature, is for organization

```rust
struct User {
    first_name: String,
    last_name: String,
    age: u64,
}

// To define the function within the context of User, we start an impl (implementation) block
// And change the first (and in this case, only) parameter to be self
impl User {
    fn full_name(&self, nickname: &str) -> String {
        format!("{} {} aka {}", self.first_name, self.last_name, nickname)
    }

    fn can_drive(&self) -> bool {
        if self.age >= 18 {
            true
        } else {
            false
        }
    }
}

fn main() {
    let user1 = User {
        first_name: String::from("Foo"),
        last_name: String::from("Bar"),
        age: 18,
    };

    println!("{}", user1.full_name("Bugsy")); // Returns "Foo Bar aka Foopub"
    println!("This user can drive: {}", user1.can_drive()); // Returns "This user can drive: true"
}
```

### Associated functions

* To call this associated function, we use the `::` syntax with the struct name
* Define functions within `impl` blocks that don't take `self` as a parameter

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }
}

fn main() {
    let sq = Rectangle::square(3);
}
```

## Statements and expressions

* Statements are instructions that perform some action and do not return a value
* Statements end with `;`
* Expressions evaluate to a resulting value
* Expressions do not include an ending `;`

```rust
let y = 6; // Statement
y + 1 // Expression
```

## Conditions

```rust
let x = 1;

// Ternary condition
if x == 1 { "One" } else { "Other" };

// Condition blocks
let number_to_s = if x == 1 {
  "One"
}
else if x == 2 {
  "Two"
}
else {
  "Three"
}
```














