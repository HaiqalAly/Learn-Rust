# This is where I put the example and code snippets from what I learned in Rustlings exercises.

### 00. Intro
```rust
fn main() {
    let greeting = "Hello, world!";
    println!("Hello, world!"); // prints Hello, world! to the console and adds a newline
    print!("Greeting: {}", greeting); // prints Greeting: Hello, world!
}
```

### 01. Variables
```rust
fn main() {
    let mut money = 10; // this is mutable (can be changed)
    println!("Current money: {}", money);
    money = 20;
    println!("Money now: {}", money);

    let money = money + 5; // shadowing the previous variable
    println!("After shadowing, money: {}", money);

    let id = 100; // immutable variable
    // id = 200; // this would cause a compile-time error

    const MAX_POINTS: u32 = 100_000; // constant with type annotation
    println!("Max points: {}", MAX_POINTS);
}
```

### 02. Functions
```rust
// This function takes two parameters and returns their difference
fn subtraction(a: i32, b: i32) -> i32 {
    a - b 
}

fn main() {
    let num1: i32 = 10;
    let num2: i32 = 5;
    let number: i32 = subtraction(num1, num2); // calling the function
    println!("{} - {} = {}", num1, num2, number);
}
```

### 03. If
```rust
fn verification(password: &str) -> &str {
    // First, determine the value of passwords based on the input password
    let passwords: i32 = if password == "rustisawesome" {
        0
    } else if password == "ihaterust" {
        1
    } else if password == "iloverust" {
        2
    } else {
        3
    };

    // Now use the value of passwords to determine the response
    if passwords == 0 {
        "Indeed it is, go ahead and enjoy your time here, new Rustacean"
    } else if password == 1 {
        "How dare you?"
    } else if password == 2 {
        "Really?"
    } else {
        "What?"
    }
}

fn main() {
    // Test the verification function with a sample password
    let entered_password: &str = "rustisawesome";
    let response: &str = verification(entered_password);
    println!("Password is: {}", response);
}
```