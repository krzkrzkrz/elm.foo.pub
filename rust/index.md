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

## Boolean & conditions

* `true` and `false`
* The Boolean type in Rust is specified using `bool`

```rust
let is_one = 1 == 1;

println!("{}", is_one); // true

// With explicit type annotation
let false_hood: bool = false;
```

## Tuples

* Grouping together some number of other values with a variety of types

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);

// Or
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
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

    // The syntax `..` specifies that the remaining fields not explicitly set should have the same value as the fields in the given instance
    let mut user2 = User {
        email: String::from("user2@example.com"),
        username: String::from("user2"),
        ..user1
    };
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

    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x);
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














