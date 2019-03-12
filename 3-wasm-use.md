## Use cases today 
1. Deliver existing applications over the web, such as games, 3D Graphics... C++ mostly
2. Develop for the web in the developers' language of choice
3. Accelerate hot code portions of ordinary JS apps
4. In the backend
5. In other areas than the web
5. Use as lib


it will be compiled at runtime


Compiler toolchains:

Rust to Wasm: 

C or C++ to Wasm: 

C --> LLVM IR // clang   
LLVM IR --> Wasm // LLVM Wasm was backend or Emscripten  using asm2wasm 


it will be compiled at runtime

What about wasm to the target machine's assembly code?  
The browser will take care of that.


## Get started!


## What languages are targeted by WASM today?

Almost any language that you think of can target WASM at the moment - they have just got different levels of maturity.

1. C++ is highly mature, because it was used throughout the development of WASM and asm.js.
2. Rust is gaining maturity quite quickly, because the nature of Rust makes it easy to target Wasm, e.g. Rust’s ownership model
3. Java and C# (and JavaScript as well) need a garbage collector and threading.

But WASM doesn’t use a garbage collector, so a common approach is to take a garbage collector and compile it to WASM. You can find C++ garbage collector implementations, and you can compile and ship that as part of your application. That’s going to add extra size, bloat and is pretty inefficient. So At some point in the future, WASM will likely support garbage collection. Maybe: rather than having its own garbage collector, it will interact with the host’s garbage collector.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

And at the moment WASM's threading model is the same as JavaScript's: a single thread of execution. When you invoke a WASM function, your JavaScript virtual machine yields to WASM. So you won’t have JavaScript and WASM running in parallel. You can have web workers, just like you can in JavaScript, so you can parallelise like that.

// wasm can support many compiled languages, certainly the static ones right now — particularly the ones that use LLVM. Microsoft has their own compiler so they’ll be doing wasm from a different compiler framework, but that’s great. The more, the merrier.

Certainly GCC or similar could generate wasm, but I think to get to the dynamic languages, like I mentioned Dart, or Ruby, or Python, even JavaScript — that’s gonna require some extensions that I mentioned earlier, like: garbage collection hooks, JIT support, things like that. Otherwise they just won’t be competitive.

There’s good precedent. The JVM grew over many years, thanks to John Rose grew things like `invokedynamic` and other hooks for just in time compilation optimizations like polymorphic inline caching so the JVM is actually a credible dynamic language platform.

All of these runtimes have become polyglot VMs — JavaScript VMs. Java hasn’t died just because the JVM now supports Clojure, and Scala, and other languages. We’re almost at the second golden age of programming languages, you know, take Rust, Haskell, Idris, and other languages.

The more the merrier, I say. It’s not gonna become the tower of Babel because I think JavaScript will be the lingua franca of the browser, today and tomorrow. If you’re writing front-end code or really anything that’s not on the critical path when you profile.

https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723


### x to wasm

WASM is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

- Write native code: C, C++ or Rust
- Compile it to a wasm module ; currently LLVM targets work best. The compiler tool chain that currently has the most support for WebAssembly is called LLVM. There are a number of different front-ends and back-ends that can be plugged into LLVM.

Once the module is fetched, it will be compiled at runtime.

Sources: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

NB:
Most WebAssembly module developers will code in languages like C and Rust and then compile to WebAssembly, but there are other ways to create a WebAssembly module:

- use TypeScript (experiemental)
- code in the text representation of WebAssembly directly.

## 3 JS to WASM

## 4

TBD

