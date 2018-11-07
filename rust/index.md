# Rust Journey

[Rust](https://www.rust-lang.org) A systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.

## New project

```console
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

## Strings

* In Rust, strings are a more complicated data structure, than is apparent in other programming languages

### String concatenation

```rust
let hello = "hello";
let world = "world";

println!("{} {}", hello, world);
```

### Strings and characters

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

### More on strings

```rust
fn main() {
    let mut s1 = "foo".to_string(); // Creates a String
    s1.push_str("bar"); // Appends bar

    // Create a String from a string literal
    let mut s2 = String::from("initial contents");

    // Creates a new, empty String
    let mut s3 = String::new();

    // Creates a reference to a String (&str)
    // Returns error: no method named push_str found for type &str in the current scope
    let mut s4 = "foo";
    s4.push_str("bar");

    // Above must be converted to a String first, before using push_str
    let s5 = "foo";
    let mut s6 = s5.to_string();
    s6.push_str("ba"); // Appends ba
    s6.push('r'); // Appends a single character
    println!("{}", s6); // Returns "foobar"
}
```

### Concatenating strings

Using the `+` operator to combine `String`s

```rust
let s1 = String::from("Hello ");
let s2 = String::from("amazing ");
let s3 = String::from("world!");
let s4 = s1 + &s2 + &s3; // s7 has been moved here and can no longer be used
println!("{}", s4); // Returns "Hello amazing world!""
```

The reason `s1` is no longer valid after the addition and the reason we used a reference to `s2` has to do with the signature of the method `add`

Which looks something like:

```rust
fn add(self, s: &str) -> String { ... }
```

### `format!`

* The `format!` macro works in the same way as `println!`
* Instead of printing the output to the screen, it returns a `String` with the contents
* The version of the code using `format!` is much easier to read and doesn't take ownership of any of its parameters

```rust
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");

let s = format!("{}-{}-{}", s1, s2, s3);
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

## Enums

* Values can only be one of the variants
* Each variant can have different types and amounts of associated data.

`enum` in its simplest form:

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

fn main() {
    let home = IpAddr::V4(127, 0, 0, 1);
    let loopback = IpAddr::V6(String::from("::1"));
}
```

A more complicated structure (with a comparison to a `struct`)

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

If the above following were to be constructed just using a `struct`, then it would look like:

```rust
struct QuitMessage; // Unit struct
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // Tuple struct
struct ChangeColorMessage(i32, i32, i32); // Tuple struct
```

`enums` have the advantage of grouping up several variants into one entity

## Option type

* Rust does not have `nulls`
* Rust has an enum that can encode the concept of a value being present or absent

It is defined by the standard library as:

```rust
enum Option<T> {
    Some(T),
    None,
}
```

Dont need to bring it into scope explicitly. You can use `Some` and `None` directly without the `Option::` prefix:

```rust
let some_number = Some(5);
let some_string = Some("a string");

let absent_number: Option<i32> = None;
```

## Match

* Compare a value against a series of patterns and then execute code based on which pattern matches

```rust
fn main() {
    println!("{}", get_string(Some(1))); // Returns "one"
}

fn get_string(number: Option<i32>) -> &'static str {
    match number {
        Some(1) => "one",
        Some(2) => "two",
        Some(3) => "three",
        Some(4) => "four",
        Some(5) => "five",
        _ => "Not in the list",
    }
}
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
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let sq = Rectangle::square(3);

    // Returns:
    // Rectangle {
    //    width: 3,
    //    height: 3
    //}
    println!("{:#?}", sq);
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

fn main() {
    let home = IpAddr::V4(127, 0, 0, 1);
    let loopback = IpAddr::V6(String::from("::1"));
}
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

## Modules

* `mod` keyword declares a new module
* By default, functions, types, constants, and modules are private. The `pub` keyword makes an item public and therefore visible outside its namespace.
* The `use` keyword brings modules, or the definitions inside modules, into scope

```console
cargo new communicator --lib // Creates a new module
cd communicator
```

Notice: Cargo generated src/lib.rs instead of src/main.rs

### Sample module (in `src/lib.rs`, multiple modules with the function name `connect`)

* Call `server::connect` or `client::connect` respectively

```rust
mod server {
    fn connect() {}
}

mod client {
    fn connect() {}
}
```

### Module inside a module

* Call `server::connect` or `server::client::connect` respectively

```rust
mod server {
    fn connect() {
    }

    mod client {
        fn connect() {
        }
    }
}
```

### Module loading

```rust
// src/lib.rs
mod client;
mod server;
```

Note that we dont need a `mod` declaration. It was already declared `src/lib.rs`.

```rust
// src/client.rs
fn connect() {
  // Some code here
}
```

```rust
// src/server.rs
fn server() {
  // Some code here
}
```

### Module filesystems

* If a module named `foo` has no submodules, you should put the declarations for `foo` in a file named `foo.rs`
* If a module named `foo` does have submodules, you should put the declarations for `foo` in a file named `foo/mod.rs`

```console
└── foo
    ├── bar.rs (contains the declarations in `foo::bar`)
    └── mod.rs (contains the declarations in `foo`, including `mod bar`)
```

### Privacy / public rules

```rust
pub mod a {
    pub fn public_function() {
        println!("Here");
    }

    fn private_function() {
        println!("Here");
    }

    pub mod series {
        pub mod of {
            pub fn nested_modules() {
                println!("Here");
            }
        }
    }
}

use a::series::of;

fn main() {
    a::public_function(); // Returns "Here"
    a::series::of::nested_modules(); // Returns "Here"
    of::nested_modules()
    a::private_function(); // Returns error: function `private_function` is private
}
```

### Compiling modules

Use `cargo build` instead of `cargo run` because we have a library crate rather than a binary crate

## `use` keyword

* Shortens lengthy function calls by bringing the modules of the function you want to call into scope
* Can be used against `enums`

```rust
pub mod a {
    pub mod really {
        pub mod long {
            pub mod list {
                pub mod of {
                    pub fn nested_modules() {
                        println!("Here");
                    }
                }
            }
        }
    }
}

enum TrafficLight {
    Red,
    Yellow,
    Green,
}

use TrafficLight::{Red, Yellow};
use a::really::long::list::of;

fn main() {
    of::nested_modules(); // Returns "Here"

    let red = Red;
    let yellow = Yellow;
    let green = TrafficLight::Green;
}
```

## Vectors

```rust
// Creating a new, empty vector to hold values of type i32
let v: Vec<i32> = Vec::new();

// Creating a new vector to hold values of type i32
let v = vec![1, 2, 3];

// Updating a vector
let mut v = Vec::new();

// Use the push method to add values to a vector
v.push(5);
v.push(6);
v.push(7);
v.push(8);

// Reading elements
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2]

// Handling out of bounds
let v = vec![1, 2, 3, 4, 5];
let v_index = 10;

match v.get(v_index) {
    Some(_) => { println!("Reachable element at index: {}", v_index); },
    None => { println!("Unreachable element at index: {}", v_index); }
} // Returns None

let does_not_exist = &v[100]; // Returns an error
let does_not_exist = v.get(100); // Returns None

// Iterating over a vector
let v = vec![100, 32, 57];

for i in &v {
    println!("{}", i);
}

// Iterating over a vector and making changes
let mut v = vec![100, 32, 57];

for i in &mut v {
    *i += 50;
}
```

## Hash maps

* Useful when you want to look up data not by using an index, as you can with vectors, but by using a key that can be of any type

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

// Iterate over a hash map
for (key, value) in &scores {
    println!("{}: {}", key, value);
}
// Returns:
// Yellow: 50
// Blue: 10

// Accesing a key in the hash map
let team_name = String::from("Blue");
let score = scores.get(&team_name);

println!("{:?}", score); // Returns Some(10)
println!("{:?}", scores); // Returns {"Blue": 10, "Yellow": 50}

// Overwriting a value
let mut teams = HashMap::new();
teams.insert(String::from("Rangers"), 2);
teams.insert(String::from("Falcons"), 1);

println!("{:?}", teams); // Returns {"Rangers": 2, "Falcons": 1}

teams.insert(String::from("Falcons"), 2);
println!("{:?}", teams); // Returns {"Rangers": 2, "Falcons": 1}

// Insert if key has no value
let mut groceries = HashMap::new();
groceries.insert(String::from("Apples"), 1);

groceries.entry(String::from("Apples")).or_insert(10);
groceries.entry(String::from("Oranges")).or_insert(1);

println!("{:?}", groceries); // Returns {"Apples": 1, "Oranges": 1}

// A more complex example
let text = "hello world wonderful world";

let mut map = HashMap::new();

for word in text.split_whitespace() {
    let count = map.entry(word).or_insert(0); // Returns a mutable reference (&mut V)
    *count += 1; // In order to assign to that value, we must first dereference count using the asterisk (*)
}

println!("{:?}", map); // Returns: {"world": 2, "wonderful": 1, "hello": 1}
```

## Error handling

### `panic!`

Force a panic:

```rust
panic!("crash and burn"); // Will cause an immediate panic
```

Running with backtrace:

```rust
let v = vec![1, 2, 3];
v[99];
```

```shell
$ env RUST_BACKTRACE=1 cargo run
```

### Recoverable Errors with `Result`

If file doesn't exist, create it. And if creation succeeds, return file
Else, panic with a message

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let f = File::open("hello.txt");

    let f = match f {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Tried to create file but there was a problem: {:?}", e),
            },
            other_error => panic!("There was a problem opening the file: {:?}", other_error),
        },
    };
}
```

### `.expect()`

Returns: `thread 'main' panicked at 'Failed to open hello.txt: ...`

```rust
use std::fs::File;

fn main() {
    let f = File::open("hello.txt").expect("Failed to open hello.txt");
}
```

## Generic types

### In `struct`s

```rust
struct Point<T, U> {
    x: T,
    y: U,
}

fn main() {
    let both_integer = Point { x: 5, y: 10 };
    let both_float = Point { x: 1.0, y: 4.0 };
    let integer_and_float = Point { x: 5, y: 4.0 };
}
```

###  In `enum`s

```rust
enum Option<T> {
    Some(T),
    None,
}

enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

### In methods

```rust
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

## Traits

* Functionality a particular type has and can share with other types

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct FacebookMessage {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

pub struct TwitterMessage {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for FacebookMessage {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

impl Summary for TwitterMessage {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

let twitter_message = TwitterMessage {
    username: String::from("foobar"),
    content: String::from("Lorem ipsum dolor"),
    reply: false,
    retweet: false,
};

println!("1 new tweet: {}", twitter_message.summarize()); // Returns: "1 new tweet: foobar: Lorem ipsum dolor"
```

### Trait defaults

```rust
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}

let article = NewsArticle {
    headline: String::from("Penguins win the Stanley Cup Championship!"),
    location: String::from("Pittsburgh, PA, USA"),
    author: String::from("Iceburgh"),
    content: String::from("The Pittsburgh Penguins once again are the best
    hockey team in the NHL."),
};

println!("New article available! {}", article.summarize()); // Returns: "New article available! (Read more...)"
```

### Traits within traits

```rust
pub trait Summary {
    fn summarize_author(&self) -> String {
        format!("@{}", self.username)
    }

    fn summarize(&self) -> String {
        format!("(Read more from {}...)", self.summarize_author())
    }
}

// ...

println!("1 new tweet: {}", twitter_message.summarize());
```

## 

```rust
```

## 

```rust
```

## 

```rust
```

## 

```rust
```




