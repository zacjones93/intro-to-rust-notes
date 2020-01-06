# intro-to-rust-notes


## Notes

[https://doc.rust-lang.org/book/](https://doc.rust-lang.org/book/)

anything that's related to your local tool chain - you use rust up

cargo is for package management and complitation

rust macros use ! at the end println!() - allow you to extend the language semantics- in a way

Any reason why has to have main function?

main() is an entry point into your program - you have to have it, the compiler requires it

main is telling the compiler where to start from think of it as your index.html in your app.

for specific rust errors, you can get a more detailed explanation with —explain

cargo new say-my-name

cargo will generate the starting boilerplate for your beginning rust app (hello world)

`Cargo.toml` is the package.json of Rust crates

toml is a super set of yaml which is a superset of JSON

→ all yaml is json, and all toml is json

[https://tom.preston-werner.com/](https://tom.preston-werner.com/)

`cargo build`

cargo lets you compile your project for different environments: dev, production,  specific environments

`cargo run` - runs cargo build then runs the code

`cargo clean` removes targets

functions in rust have implicit returns 

    pub fn sum(a: u32, b: u32) -> u32 {
    	a + b
    }

would this cast something more generic to u32, or does it need to be a u32 when being passed in?

The basic type you set is based on how large you expect the numbers to be. You have to set an explicit type

There's a module system in rust. 

    mod foo;

Everything that exposed on that module is accessed through the namespace.

    foo::sum(3,4);

you can expose modules that are within other modules

    pub mod bar;
    
    pub fn sum(a: u32, b: u32) -> u32 {
    	a + b
    }

then it can be accesed as `foo::bar::some_fn`

quick access to a function can be `use foo::sum as add;` and `add(3, 4);`

so pub = export and mod = import?

`mod` and `use` can be considered as `import` from javascript

- Everything is private by default
- variable are immutable by default in Rust

    fn main() {
    	let name = "Pascal";
    
    println!("{}", name);
    }

`"{}"` is a placeholder but also a formatter to print a given value. Types like Structs can't be printed with the default formatter and need more configuration

The output can be configured. So `println` can take `"{:?}"` which will print out a struct in a 'debuggable' way → a human readable way. For a struct, you need to add `#[derive(Debug)]` to implement the debug trait

[https://doc.rust-lang.org/std/fmt/#formatting-traits](https://doc.rust-lang.org/std/fmt/#formatting-traits)

You can implement your own trait, in this case `Debug` for a specific Type, in our case `Person`

    impl std::fmt::Debug for Person {
    
    }
    
    ----------
    
    use std::fmt::Debug;
    
    impl Debug for Person { 
    
    
    }

Look up in the docs how to implement the Debug instance for your type. It expects a function  that might 

- Rust doesn't throw exceptions. Rust has the type of `Result` that makes you be explicit about handling errors

- You can implement methods on structs

    impl Person {
      fn print_name(&self) -> String {
    		println!("{} {}", self.firstname, self.name);
    	}
    }

`()` is a unit type in Rust - void

`Foo::myMethod()`

you want an associated function when you want a function in a certain namespace but that function doesn't depend on the specific instance

If you want to mutate a variable you have to explicitly set that

    let mut name = "Pascal";

If it is immutable, is it really a variable?

yes. A `const` is static through whole lifetime of the application

variables can be apart of an expression, when they are set you know what it will be becasue  it's immutable. But at compile time you don't know what the variable is

from `read_line` returns bytes so the resulting type is `usize` which is as big as you want

Anything that is within a scope that is not reference will be dropped after that scope is done executing. Unless something is returned. 

If you call a function with a variable, that variables ownership is moved to the called function. If the function doesn't return that variable, it will get dropped.

What makes Rust’s value dropping not garbage collection?

it compiles the code in a way that Rust knows at each point in time during the programs lifetime when a value is needed so it 'knows' when to drop a value

This makes you have to be very explicit to tell the compiler what you expect something to be

`Result` always returns a value of type `T` or an `Error`, similar to a Promise in JS

`stdin` returns the type `usize` 

you can `unwrap` from a `Result` to get at value
