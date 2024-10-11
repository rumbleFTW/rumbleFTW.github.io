---
title: "ffi basics in rust"
categories: [programming]
date: 2024-10-12 01:40:56 +0530
toc: true
description: >-
  An introduction to FFI in Rust.
tags: [programming, rust]
---

# Understanding FFI in Rust: Bridging the Gap Between Languages

Foreign Function Interface (FFI) is a powerful mechanism that allows code written in one programming language to call and interact with code written in another language. In the Rust ecosystem, FFI is particularly useful for interfacing with existing C and C++ libraries, leveraging legacy code, or optimizing performance-critical sections. This blog post will dive deep into the concept of FFI in Rust, exploring its benefits, challenges, and implementation details.

## What is FFI?

FFI, or Foreign Function Interface, is a way for code written in one programming language to call code written in another programming language. It's a bridge that allows different programming languages to communicate and work together within a single application.

In the context of Rust, FFI most commonly refers to the ability to call C or C++ functions from Rust code, or to expose Rust functions to be called from C or C++. This interoperability is crucial for several reasons:

1. **Leveraging existing libraries**: Many well-established libraries are written in C or C++. FFI allows Rust programs to use these libraries without rewriting them.
2. **Performance optimization**: For certain performance-critical tasks, it might be beneficial to implement them in C or C++ and call them from Rust.
3. **System integration**: Many operating system APIs are exposed as C interfaces, which can be accessed through FFI.

## How FFI Works in Rust

Rust's FFI capabilities are built on top of the C Application Binary Interface (ABI). This means that Rust can seamlessly interact with any language that also adheres to the C ABI, which includes C and C++.

### Key Concepts

1. **Unsafe Rust**: FFI calls are inherently unsafe because Rust cannot guarantee the safety of foreign code. Therefore, FFI functions must be called within `unsafe` blocks.

2. **Linkage**: To use a foreign function, Rust needs to know where to find it. This is typically done by linking to a shared or static library.

3. **Type Mapping**: Rust types need to be mapped to C types and vice versa. Rust provides primitive types that correspond to C types, and more complex types can be mapped using structs and enums.

4. **Calling Convention**: The way function arguments are passed and results are returned needs to be consistent between languages. Rust uses the C calling convention by default for external functions.

## Implementing FFI in Rust

Let's walk through the process of implementing FFI in Rust, using a simple example project as a reference. We'll be referring to the [math_ops_ffi](https://github.com/rumbleFTW/math_ops_ffi) repository, which demonstrates how to call C++ functions from Rust using FFI.

### 1. Declaring Foreign Functions

To use a C++ function in Rust, you first need to declare its signature. This is typically done in an `extern` block:

```rust
extern "C" {
    fn add(a: i32, b: i32) -> i32;
    fn subtract(a: i32, b: i32) -> i32;
}
```

The `"C"` specifies that these functions use the C calling convention.

### 2. Calling Foreign Functions

Once declared, you can call these functions in your Rust code. Remember, they must be called within an `unsafe` block:


```rust
// src/main.rs
fn main() {
    let result_add = unsafe { add(5, 3) };
    println!("5 + 3 = {}", result_add);

    let result_subtract = unsafe { subtract(10, 4) };
    println!("10 - 4 = {}", result_subtract);
}
```


### 3. Building and Linking

To make the FFI work, you need to build the C/C++ code and link it with your Rust project. This is typically done using a build script (`build.rs`):


```rust
// build.rs
use std::env;
use std::path::PathBuf;

fn main() {
    println!("cargo:rustc-link-search=native=lib");
    println!("cargo:rustc-link-lib=static=math_ops");

    let bindings = bindgen::Builder::default()
        .header("cpp/include/math_ops.h")
        .parse_callbacks(Box::new(bindgen::CargoCallbacks::new()))
        .generate()
        .expect("Unable to generate bindings");

    let out_path = PathBuf::from(env::var("OUT_DIR").unwrap());
    bindings
        .write_to_file(out_path.join("bindings.rs"))
        .expect("Couldn't write bindings!");
}
```


This script does several important things:
- It tells Cargo where to find the compiled C++ library.
- It uses `bindgen` to automatically generate Rust bindings for the C++ functions.

### 4. Generating Bindings

The `bindgen` crate is a powerful tool that automatically generates Rust FFI bindings to C and C++ libraries. It parses C/C++ header files and creates corresponding Rust code, saving you from manually writing FFI declarations.

### 5. Compiling the C++ Code

For the C++ side, you typically use a build system like CMake:


```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.10)
project(RustCppFFI VERSION 1.0)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)

add_library(math_ops STATIC
    cpp/src/math_ops.cpp
)

target_include_directories(math_ops PUBLIC
    ${CMAKE_SOURCE_DIR}/cpp/include
)

target_compile_options(math_ops PRIVATE -Wall -Wextra)
```


This CMake configuration builds the C++ code as a static library that can be linked with the Rust code.

## Challenges and Considerations

While FFI is powerful, it comes with its own set of challenges:

1. **Safety**: FFI code is inherently unsafe. You need to be careful about memory management, type conversions, and adhering to the contract of the foreign functions.

2. **Portability**: FFI code can be less portable, as it may depend on platform-specific libraries or conventions.

3. **Maintenance**: Changes in the foreign code may require updates to your Rust bindings and vice versa.

4. **Performance Overhead**: While generally minimal, there can be some performance overhead in crossing the FFI boundary, especially for frequent, small function calls.

## Conclusion

FFI in Rust opens up a world of possibilities, allowing Rust programs to interface with a vast ecosystem of existing C and C++ libraries. While it requires careful handling due to its unsafe nature, FFI is a powerful tool in a Rust developer's toolkit.

By understanding the concepts and implementation details of FFI, you can effectively bridge the gap between Rust and other languages, creating robust, efficient, and interoperable software systems.

Remember, the key to successful FFI implementation lies in understanding both Rust and the foreign language you're interfacing with, as well as the intricacies of the FFI mechanism itself. With careful design and implementation, FFI can be a game-changer in your Rust projects.
