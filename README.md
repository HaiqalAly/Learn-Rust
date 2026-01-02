# 🦀 My Rustling Journey
This repository contains my Rust learning journey with Rustlings exercises. My goal is to get comfortable with Rust's syntax and core concepts like ownership and borrowing.

## 📊 Progress
0. [✔️] Intro
1. [✔️] Variables
2. [✔️] Functions
3. [✔️] If

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