+++
title = "Chamos"
+++

Chamos is an experimental stack-based programming language with static typing.
I'm working on the first version of the compiler, written in Rust. Its syntax
is similar to Forth or UXN, but with more complexity added for defining
functions, control flow, etc.

In Chamos, functions operate on the top of the stack rather than on variables.
Every item on the stack has a type - a function's "arguments" are a
requirement for what the top of the stack must look like for that function to
be called, called it's *stack scope*. The body of the function can
then manipulate the stack directly, using keywords like `drop` and `swap`, or
work with references to named items in the scope. A function cannot manipulate
the stack below its scope, ensuring that the stack effect of every function
is known.

Here's a hello world program for x86 Linux - many of these functions will
become part of the standard library:

```
fn exit ( code u64 ) {
    60 swap 0 0 syscall
}

fn print ( char u8 ) {
    1 1 char 1 syscall
}

fn print ( text &str ) {
    1 1 text.first text.len @ syscall
}

fn println ( text &str ) {
    print
    10u8 print drop
}

fn main () {
    "Hello, world!" println
    0 exit
}
```

## To-do:

* Control flow
* Structs & enums
* Modularisation & standard library