# 🦀 My Rustling Journey
This repository contains my Rust learning journey with Rustlings exercises. My goal is to get comfortable with Rust's syntax and core concepts like ownership and borrowing.

## 📊 Progress
0. [✔️] Intro
1. [✔️] Variables
2. [✔️] Functions
3. [✔️] If
4. [✔️] Primitive Types
5. [✔️] Vecs
6. [✔️] Move Semantics
7. [✔️] Structs

## 📝 Notes

### 00. Intro
- Rust uses `print!` and `println!` macros for console output
- `println!` automatically adds a newline at the end
- Use `{}` as placeholders for formatting values

### 01. Variables
- Variables are immutable by default in Rust
- Use `let` to declare a variable
- Add `mut` keyword to make a variable mutable: `let mut x = 5;`
- Can shadow variables by re-declaring with `let`
- Constants use `const` and must have a type annotation

### 02. Functions
- Functions are defined with `fn` keyword
- Use snake_case for function names
- Parameters must have type annotations: `fn add(x: i32, y: i32)`
- Return type specified with `->`: `fn add(x: i32, y: i32) -> i32`
- Last expression (without semicolon) is the return value
- Use `return` keyword for early returns

### 03. If
- Conditional statements use `if`, `else if`, and `else`
- Conditions must evaluate to a boolean (`true` or `false`)
- Can assign the result of an `if` expression to a variable

### 04. Primitive Types
- Booleans (`bool`): `true` or `false`, used in conditionals
- Characters (`char`): single quotes `'C'`, `'😉'`, has methods like `.is_alphabetic()`
- Arrays & slices: fixed size, slice syntax `&a[1..4]` (end exclusive)
- Tuples: multiple types `("name", 3.5)`, access with `tuple.0`, `tuple.1`

### 05. Vecs
- Vectors (`Vec<T>`): growable arrays, create with `vec![1, 2, 3]` macro
- Unlike arrays, vectors can change size at runtime
- Add elements with `.push()`, create empty with `Vec::new()`
- Loop through slice `&[i32]` thwi `for &element in input`
- Iterator pattern: `.iter().map(|x| x * 2).collect()` transforms elements

### 06. Move Semantics
- Ownership: Each value has a single owner; when owner goes out of scope, value is dropped
- Move: Passing a value to a function transfers ownership (moves it) by default
- Mutability: Parameters can be `mut` to allow modification: `fn fill_vec(mut vec: Vec<i32>)`
- Clone: Use `.clone()` to create a copy and keep the original accessible
- Borrowing: Mutable borrows (`&mut`) must be used one at a time, no overlapping borrows
- References vs Ownership: Use `&String` to borrow without taking ownership; use `String` to take ownership
- Key concepts: choosing between borrowing (`&T`) and ownership transfer depending on whether the function needs to consume the value

### 07. Structs
- Defined classic, tuple, and unit structs in [exercises/07_structs/structs1.rs](exercises/07_structs/structs1.rs)
- Instantiated each kind; accessed named fields (like `.red`) and tuple indices (`.0`, `.1`, `.2`); formatted a unit struct with `{:?}`
- Used struct update syntax (`..template`) in [exercises/07_structs/structs2.rs](exercises/07_structs/structs2.rs) to build a new `Order` from a template while overriding `name` and `count`
- Implemented methods and an associated constructor in [exercises/07_structs/structs3.rs](exercises/07_structs/structs3.rs): `is_international()` comparing countries, and `get_fees()` multiplying `cents_per_gram * weight_in_grams`
- Practiced method receivers with `&self`

### Quiz 1
- Wrote function with `u32` params and return type
- Applied bulk discount logic: if qty > 40 then 1 rustbuck/apple, else 2 rustbucks/apple
- Used `if/else` expression as return value (no semicolon needed)