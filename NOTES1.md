## 00. Intro
- Rust uses `print!` and `println!` macros for console output
- `println!` automatically adds a newline at the end
- Use `{}` as placeholders for formatting values

## 01. Variables
- Variables are immutable by default in Rust
- Use `let` to declare a variable
- Add `mut` keyword to make a variable mutable: `let mut x = 5;`
- Can shadow variables by re-declaring with `let`
- Constants use `const` and must have a type annotation

## 02. Functions
- Functions are defined with `fn` keyword
- Use snake_case for function names
- Parameters must have type annotations: `fn add(x: i32, y: i32)`
- Return type specified with `->`: `fn add(x: i32, y: i32) -> i32`
- Last expression (without semicolon) is the return value
- Use `return` keyword for early returns

## 03. If
- Conditional statements use `if`, `else if`, and `else`
- Conditions must evaluate to a boolean (`true` or `false`)
- Can assign the result of an `if` expression to a variable

## 04. Primitive Types
- Booleans (`bool`): `true` or `false`, used in conditionals
- Characters (`char`): single quotes `'C'`, `'😉'`, has methods like `.is_alphabetic()`
- Arrays & slices: fixed size, slice syntax `&a[1..4]` (end exclusive)
- Tuples: multiple types `("name", 3.5)`, access with `tuple.0`, `tuple.1`

## 05. Vecs
- Vectors (`Vec<T>`): growable arrays, create with `vec![1, 2, 3]` macro
- Unlike arrays, vectors can change size at runtime
- Add elements with `.push()`, create empty with `Vec::new()`
- Loop through slice `&[i32]` thwi `for &element in input`
- Iterator pattern: `.iter().map(|x| x * 2).collect()` transforms elements

## 06. Move Semantics
- Ownership: Each value has a single owner; when owner goes out of scope, value is dropped
- Move: Passing a value to a function transfers ownership (moves it) by default
- Mutability: Parameters can be `mut` to allow modification: `fn fill_vec(mut vec: Vec<i32>)`
- Clone: Use `.clone()` to create a copy and keep the original accessible
- Borrowing: Mutable borrows (`&mut`) must be used one at a time, no overlapping borrows
- References vs Ownership: Use `&String` to borrow without taking ownership; use `String` to take ownership
- Key concepts: choosing between borrowing (`&T`) and ownership transfer depending on whether the function needs to consume the value

## 07. Structs
- Defined classic, tuple, and unit structs in [exercises/07_structs/structs1.rs](exercises/07_structs/structs1.rs)
- Instantiated each kind; accessed named fields (like `.red`) and tuple indices (`.0`, `.1`, `.2`); formatted a unit struct with `{:?}`
- Used struct update syntax (`..template`) in [exercises/07_structs/structs2.rs](exercises/07_structs/structs2.rs) to build a new `Order` from a template while overriding `name` and `count`
- Implemented methods and an associated constructor in [exercises/07_structs/structs3.rs](exercises/07_structs/structs3.rs): `is_international()` comparing countries, and `get_fees()` multiplying `cents_per_gram * weight_in_grams`
- Practiced method receivers with `&self`

## 08. Enums
- Defined basic enum with unit variants in [exercises/08_enums/enums1.rs](exercises/08_enums/enums1.rs)
- Enums can have different variant types in [exercises/08_enums/enums2.rs](exercises/08_enums/enums2.rs):
  - Unit variants: `Quit` (no data)
  - Tuple variants: `Move(Point)`, `Echo(String)` (unnamed fields)
  - Struct-like variants: `Resize { width: u32, height: u32 }` (named fields)
- Pattern matching with `match` in [exercises/08_enums/enums3.rs](exercises/08_enums/enums3.rs):
  - Destructure struct variants: `Message::Resize { width, height } => ...`
  - Extract tuple data: `Message::Move(point) => ...`
  - Handle all variants exhaustively (compiler enforces this)
- Match expressions delegate to appropriate methods based on enum variant
- Enums are powerful for representing data that can be one of several types

## 09. Strings
- Two main string types: `String` (owned, heap-allocated) and `&str` (string slice, borrowed)
- Converting `&str` to `String` in [exercises/09_strings/strings1.rs](exercises/09_strings/strings1.rs): `.to_string()` method
- Converting `String` to `&str` in [exercises/09_strings/strings2.rs](exercises/09_strings/strings2.rs): use `&` to borrow
- String methods in [exercises/09_strings/strings3.rs](exercises/09_strings/strings3.rs):
  - `.trim()` removes whitespace from both ends, returns `&str`
  - `format!("{} world!", input)` concatenates strings, returns `String`
  - `.replace("old", "new")` replaces substrings, returns new `String`
- Multiple ways to create `String` in [exercises/09_strings/strings4.rs](exercises/09_strings/strings4.rs):
  - `.to_string()` - converts to owned String
  - `String::from()` - creates String from literal
  - `.to_owned()` - clones into owned String
  - `.into()` - type conversion (requires type inference)
  - `format!()` - string interpolation
- String slicing `&String[0..1]` returns `&str` (byte indexing, not character indexing)
- Methods like `.trim()`, `.replace()`, `.to_lowercase()` return different types based on whether they modify

## 10. Modules
- Visibility and public API in [exercises/10_modules/modules1.rs](exercises/10_modules/modules1.rs): made `get_secret_recipe()` private and exposed `make_sausage()` with `pub`, then called `sausage_factory::make_sausage()` from `main`.
- Aliases and re-exports in [exercises/10_modules/modules2.rs](exercises/10_modules/modules2.rs): used `pub use` with `as` to re-export `fruits::PEAR` and `veggies::CUCUMBER` as `fruit` and `veggie`, so consumers can access `delicious_snacks::fruit` and `delicious_snacks::veggie`.
- Scoped imports in one line in [exercises/10_modules/modules3.rs](exercises/10_modules/modules3.rs): brought `SystemTime` and `UNIX_EPOCH` from `std::time` into scope with `use std::{time::SystemTime, time::UNIX_EPOCH};` and printed seconds since the Unix epoch.

## 11. Hashmaps
- HashMaps store key-value pairs with fast lookup: `HashMap<K, V>`
- Created HashMap with `HashMap::new()` in [exercises/11_hashmaps/hashmaps1.rs](exercises/11_hashmaps/hashmaps1.rs): used `.insert()` to add `String` keys and `u32` values
- Entry API in [exercises/11_hashmaps/hashmaps2.rs](exercises/11_hashmaps/hashmaps2.rs): `.entry(key).or_insert(value)` inserts only if key doesn't exist, preventing overwrites
- Custom structs as values in [exercises/11_hashmaps/hashmaps3.rs](exercises/11_hashmaps/hashmaps3.rs): `.entry(key).or_default()` creates entry with `Default` trait, then mutate the returned reference
- Applied to soccer scores: tracked goals scored and conceded per team across multiple matches

## 12. Options
- `Option<T>` represents optional values: `Some(value)` or `None` (replaces null)
- Returning Options in [exercises/12_options/options1.rs](exercises/12_options/options1.rs): return `Some(T)` when value exists, `None` otherwise; extract with `.unwrap_or(default)`
- Pattern matching in [exercises/12_options/options2.rs](exercises/12_options/options2.rs): `if let Some(value) = optional` for single case, `while let Some(Some(value))` for nested Options
- Borrowing in [exercises/12_options/options3.rs](exercises/12_options/options3.rs): use `Some(ref p)` to borrow instead of moving the value out of Option

## 13. Error Handling
- `Result<T, E>` represents operations that can succeed or fail: `Ok(value)` for success, `Err(error)` for failure
- Converting from Option to Result in [exercises/13_error_handling/errors1.rs](exercises/13_error_handling/errors1.rs): changed `Option<String>` to `Result<String, String>`, replacing `None` with `Err(message)` and `Some(value)` with `Ok(value)`
- The `?` operator in [exercises/13_error_handling/errors2.rs](exercises/13_error_handling/errors2.rs): propagates errors automatically; `parse::<i32>()?` returns early with `Err` if parsing fails, otherwise unwraps the `Ok` value
- Propagating errors in main in [exercises/13_error_handling/errors3.rs](exercises/13_error_handling/errors3.rs): changed `main()` to `main() -> Result<(), ParseIntError>` and added `Ok(())` at the end to allow using `?` operator
- Custom error types in [exercises/13_error_handling/errors4.rs](exercises/13_error_handling/errors4.rs): defined `CreationError` enum with `Negative` and `Zero` variants, used pattern matching to return appropriate error type
- Trait objects with `Box<dyn Error>` in [exercises/13_error_handling/errors5.rs](exercises/13_error_handling/errors5.rs): allows handling multiple error types by implementing the `Error` trait; `Box<dyn Error>` acts as a catch-all for any error type
- Composing custom errors in [exercises/13_error_handling/errors6.rs](exercises/13_error_handling/errors6.rs): created `ParseIntError`; used `.map_err()` to convert error types when propagating with `?`

## 14. Generics
- Defined generic vector `Vec<T>` in [exercises/14_generics/generics1.rs](exercises/14_generics/generics1.rs): explicit type annotation `Vec<i32>` needed when compiler cannot infer type from usage
- Generic structs and implementations in [exercises/14_generics/generics2.rs](exercises/14_generics/generics2.rs): defined `struct Wrapper<T>` to hold any type, and `impl<T> Wrapper<T>` to define methods for that generic type

## 15. Traits
- Implementing traits in [exercises/15_traits/traits1.rs](exercises/15_traits/traits1.rs): defined behavior using `impl Trait for Type`, adding method `append_bar` to `String`
- Trait implementations for generics in [exercises/15_traits/traits2.rs](exercises/15_traits/traits2.rs): implemented the trait for `Vec<String>`, demonstrating how to extend standard collection types
- Default implementations in [exercises/15_traits/traits3.rs](exercises/15_traits/traits3.rs): defined a default body for `licensing_info` in the trait so implementors share common behavior automatically
- Trait bounds with `impl Trait` in [exercises/15_traits/traits4.rs](exercises/15_traits/traits4.rs): used `fn func(arg: impl Trait)` to accept any type that implements a trait, enabling polymorphism
- Multiple trait bounds in [exercises/15_traits/traits5.rs](exercises/15_traits/traits5.rs): used `+` syntax (`impl Trait1 + Trait2`) to specify that a parameter must implement multiple traits