# The Importance of Rust with Embedded Systems<br />By Dylan Catte

<br />

## Introduction to Rust
Rust is a modern language created by the Mozilla Research Team in 2006. It boasts impressive performance numbers in throughput with a minimal memory footprint.
Rust's claim to fame is its memory safety. It uses an algorithm called a "borrow checker" to ensure that memory is properly used without causing corruption issues.
This can be used to prevent common vunlerabilities in other languages such as C++ including the infamous `Out of Bounds` errors that cause many modern computer viruses.
Rust is syntactically similar to other systems programming languages. The idea that sets it apart is that variables cannot be "borrowed" multiple times. Once a variable
enters an inner scope, it cannot be utilized outside of that scope due to safety issues. Using references to memory addresses can be used to safely use variables in
multiple scopes.

```rust
fn main() {
    let mut num = 10; // A mutable variable

    {
        let r1 = &num; // Immutable borrow
        println!("Immutable borrow: {}", r1);
        // `num` cannot be modified while `r1` exists
    } // `r1` goes out of scope here, so `num` can be borrowed mutably now

    {
        let r2 = &mut num; // Mutable borrow
        *r2 += 5; // Modify value
        println!("Mutable borrow: {}", r2);
    } // `r2` goes out of scope, so `num` can be used safely again

    println!("Final value: {}", num);
}
```
<br />

## Comparing Rust to C/C++
Rust has been generally accepted as the modern replacement for C++. On February 26th, 2024, the United States White House announced that all C++ code was to be replaced
with memory safe alternatives in the coming years, with Rust being remarked as one of the best alternatives. That [press release](https://www.whitehouse.gov/oncd/briefing-room/2024/02/26/press-release-technical-report/)
has since been taken down by the Trump Administration; however the United States' efforts to eliminate C/C++ continue with [Project TRACTOR](https://www.darpa.mil/research/programs/translating-all-c-to-rust), 
a translation layer from C to Rust. <br />

That being said, the migration from C to Rust is not due to minute reasons. Rust is significantly easier to maintain than C as it has a large ecosystem of development tools to back it such as
Clippy, an automated code optimizer. In addition to ease of development, Rust also is among the most memory safe languages, with many levels of security to prevent exploits
and vulnerabilities from occuring. Rust has some of the most rigorous compilation requirements, forcing programmers to only release the highest quality code. However, the
largest reason for the "Great Rust Migration" is its performance relative to other similar languages.
<br />

## Benchmarking Rust and C++
A good benchmark for comparing languages is their ability to compute complex algorithms. In this benchmark there will be two main algorithms: the Fibonacci Sequence and a Prime Finder Algorithm.
All of the benchmarks were performed on a Ryzen 9 5950X CPU with 64GB of RAM at 3600MHz CL16. <br />

<b>Fibonacci Sequence:</b> This test used recursive functions to calculate the fibonacci sequence up to the 40th value. This is considered among some of the
intensive computations a computer can do with a time complexity of `O(2^n)`. The code as originally created in Rust with no external dependencies, then
manually translated into the C++ equivalent. As show in Chart 1 below, Rust performs 72.14% better in Dev mode and 120.96% better in Release mode.<br />

<p align="center">
  <img src="https://github.com/user-attachments/assets/d298470f-2283-4e9c-bdae-8793347b1471" />
  <br />
  <b>Chart 1</b>
</p>
<br />

<b>Prime Finder:</b> This test used the Sieve of Eratosthenes to calculate up to the 10,000,000th prime number. This is a computationally heavy task with a time
complexity of `O(n * log(log(n)))`. The code was originally created in Rust with no external dependencies, then ported to C++ to compare. As show below in Chart 2, Rust
was significantly faster than C++, being 2176.86% faster in Dev mode and an astonishing 3706.14% faster in Release mode. This is like due to C++'s lackluster
I/O performance.<br />

<p align="center">
  <img src="https://github.com/user-attachments/assets/53831849-fcb8-4a56-b38c-65b070d2d4d3" />
  <br />
  <b>Chart 2</b>
</p>
<br />

<b>Binary Size:</b> The size of the compiled binary is also an important subject when dealing with constrained storage. Rust does extremely poorly in this area.
While C++ puts extra resources to compressing the final binary, Rust dedicates that addition computation to improving code efficiency and readability. This results
in Rust having a 827.78% larger binary for the two previous benchmarks compared to C++, as shown in Chart 3.<br />

<p align="center">
  <img src="https://github.com/user-attachments/assets/ee246cc1-b779-49a4-aa2a-26a8a5fd56f3" />
  <br />
  <b>Chart 3</b>
</p>
<br />

## Integrating Rust with Embedded Systems and Single Board Computers
Embedded Systems and Single Board Computes (SBCs) both have two things in common: they have little computational power and they have very little usable memory.
This means optimization for throughput and memory footprint are crucial when developing on these platforms. Luckily Rust excels in both of these areas.
Embedded Rust is a very experimental subset of the Rust programming language that removes the standard library and allows for significantly smaller binary sizes.
Embedded Rust programs can be only a few kilobytes in size. The main issue with Embedded Rust compared to C++ is the lack of documentation and resources for
embedded functionality such as GPIO and UART. That is rapidly changing however. Many embedded systems engineers are beginning to recognize the importance of 
Rust in this ecosystem. Recently for the Ohio Northern University Foundations of Design Showcase, the team I was a part of developed an [entire greenhouse
monitoring system](https://github.com/QPCrummer/GEM-rs) completely in Embedded Rust.
<br />

## Conclusion
C++ has real competition now. Devs no longer have to rely on the bulky, unoptimized code that C++ creates, nor do they have to worry about potential memory
vulnerabilities that are associated with C and C++. Rust is the future for not only embedded systems, but for programming as a whole. It is an extremely
versitile language with endless possibilities. It's just a matter of time until the entire world has completely oxidized.
