## 16. Lifetimes
- Lifetime annotations (`'a`) help the compiler ensure references are valid (prevent dangling pointers)
- Annotated function signatures in [exercises/16_lifetimes/lifetimes1.rs](exercises/16_lifetimes/lifetimes1.rs): `fn longest<'a>(x: &'a str, y: &'a str) -> &'a str` links output lifetime to inputs
- Fixed scope issues in [exercises/16_lifetimes/lifetimes2.rs](exercises/16_lifetimes/lifetimes2.rs): ensured data outlives its references by moving variable declaration to a wider scope
- Annotated structs in [exercises/16_lifetimes/lifetimes3.rs](exercises/16_lifetimes/lifetimes3.rs): defined `struct Book<'a>` to enforce that referenced fields (`author`, `title`) live at least as long as the struct

## 17. Tests
- Defined unit tests in a dedicated module with `#[cfg(test)]` annotation
- Imported parent module functions using `use super::*` to access code being tested
- Used `assert!(expression)` to verify boolean conditions in [exercises/17_tests/tests1.rs](exercises/17_tests/tests1.rs)
- Used `assert_eq!(left, right)` to verify equality between values in [exercises/17_tests/tests2.rs](exercises/17_tests/tests2.rs)
- Used `#[should_panic]` attribute to test that specific code paths (like invalid input) correctly panic in [exercises/17_tests/tests3.rs](exercises/17_tests/tests3.rs)

## 18. Iterators
- **Transformation & Collection**:
  - `.iter()` creates an iterator from a collection.
  - `.map()` transforms items lazily.
  - `.collect()` consumes the iterator. It can infer the return type:
    - `.collect::<Vec<_>>()`: Creates a list of results.
    - `.collect::<String>()`: Joins iterator results into a single string.
- **Handling Errors with Result**:
  - `collect()` behavior changes based on return type:
    - `Result<Vec<T>, E>`: Stops at the first error (fails fast).
    - `Vec<Result<T, E>>`: Collects all results, including success and errors.
- **Reduction**:
  - `.fold(init, op)`: Accumulates a single value from the iterator, starting with an initial value.
  - `.product()`: Specialized method to multiply all elements (concise alternative to `fold` for factorials).
  - Ranges `(1..=num)` can be used to generate sequences easily.
- **Filtering & Flattening**:
  - `.filter()`: Keeps only items matching a predicate.
  - `.values()`: Gets the values from a HashMap.
  - `.flat_map()`: Maps each element to an iterator and then flattens the nested structure (e.g., extracting values from a list of HashMaps into a single stream).
  - `.count()`: Consumes the iterator to count the remaining elements.

## 19. Smart Pointers
- **Box (`Box<T>`)**:
  - Allocates values on the heap instead of the stack.
  - **Recursive Types**: Necessary for defining types like linked lists (Cons list) where a type contains itself. Without `Box`, the size would be infinite/unknown at compile time. `Box` has a known pointer size.
  - **Usage**: `Box::new(value)` moves the value to the heap.
- **Rc (`Rc<T>`)**:
  - Reference Counted smart pointer.
  - **Multiple Ownership**: Allows multiple parts of your program to own the same data simultaneously (e.g., a "Sun" owned by multiple "Planets").
  - **Single-threaded**: ONLY for use in single-threaded scenarios. It is faster than `Arc` because it doesn't need atomic operations.
  - **Cloning**: `Rc::clone(&rc)` increments the reference count. Usually cheap (increments an integer), does not deep-copy the data.
- **Arc (`Arc<T>`)**:
  - Atomic Reference Counted.
  - **Thread-safe**: Same mechanism as `Rc` but uses atomic operations for the counter, making it safe to share across threads.
  - **Shared Ownership**: Used when multiple threads need access to the same read-only data.
  - **Usage**: `Arc::clone(&arc)` creates a new handle for another thread.
- **Cow (`Cow<T>`)**:
  - "Clone on Write".
  - **Optimization**: A smart enum that can hold either *borrowed* data (`&T`) or *owned* data (`T`).
  - **Lazy Cloning**: It keeps data borrowed (cheap) as long as you only read it. It only clones (expensive) if you try to mutate it (`.to_mut()`).
  - Useful for functions that verify data and only occasionally need to modify it.

## 20. Threads
- **Spawning**: `thread::spawn(move || { ... })` creates a new thread along with a closure containing the code to run.
  - The `move` keyword is often required to transfer ownership of variables into the thread's closure.
- **Join Handles**: `spawn` returns a `JoinHandle`.
  - Calling `.join()` blocks the current thread until the spawned thread finishes.
  - `.join()` returns a `Result`, allowing you to retrieve the value returned by the thread (or handle panics).
- **Shared Mutable State**:
  - **Arc (`Arc<T>`)**: Atomic Reference Counting. Used to share ownership of data across multiple threads.
  - **Mutex (`Mutex<T>`)**: Mutual Exclusion. Used to allow mutable access to shared data.
  - **Arc<Mutex<T>>**: The standard pattern for shared mutable state.
  - **Locking**: Call `.lock()` on the Mutex to get access to the inner data. This blocks until the lock is acquired. It returns a `MutexGuard` (wrapped in a Result) which automatically releases the lock when it goes out of scope.
- **Channels**:
  - `mpsc` (Multi-Producer, Single-Consumer) allows threads to communicate by sending messages.
  - `mpsc::channel()` returns a `(Sender, Receiver)` tuple.
  - **Cloning Senders**: To have multiple threads send to the same channel, you must `.clone()` the sender (`tx`).
  - **Ownership**: Be careful about moving data (like struct fields) into threads. You may need to destructure structs or clone specific parts *before* spawning threads to ensure each thread gets the ownership it needs.

## 21. Macros
- **Definition**: Defined using `macro_rules!` followed by the name and a block.
  - Unlike functions, macros end with `!`.
- **Matching**: Macros use a pattern matching syntax similar to `match` expressions.
  - `(patterns) => { code }`
  - Arguments are prefixed with `$` (e.g., `$val:expr` matches an expression and binds it to `$val`).
- **Scoping**:
  - Macros are lexically scoped; they must be defined *before* they are called in the file.
  - To use macros from a nested module, use `#[macro_use]` on the module declaration.
- **Arms**: Macros can have multiple "arms" to handle different arguments, separated by semicolons `;`.

---

## Quiz 1
- Wrote function with `u32` params and return type
- Applied bulk discount logic: if qty > 40 then 1 rustbuck/apple, else 2 rustbucks/apple
- Used `if/else` expression as return value (no semicolon needed)

## Quiz 2
- Built a string transformer function taking `Vec<(String, Command)>` input
- Defined enum with three variants: `Uppercase`, `Trim`, and `Append(usize)` (tuple variant)
- Used pattern matching to handle each command:
  - `Uppercase`: called `.to_uppercase()` to convert string to uppercase
  - `Trim`: called `.trim().to_string()` to remove whitespace and return owned String
  - `Append(n)`: looped `n` times pushing "bar" to a mutable string
- Imported function from module with `use crate::my_module::transformer`
- Combined concepts: enums, match expressions, vectors, string methods, modules, and move semantics

## Quiz 3
- Refactored `ReportCard` struct to support multiple grade types using generics
- Changed `grade: f32` to `grade: T` in the struct definition
- Updated `impl` block to generic implementation `impl<T: std::fmt::Display>`
- Used the `Display` trait bound to ensure the generic grade can be printed with `{}` inside `format!`
- Enabled polymorphism: `ReportCard` can now accept `f32` (numeric) or `String`/`&str` (alphabetic) grades while sharing the same printing logic