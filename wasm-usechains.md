1. Deliver existing C/C++ applications over the web (Talking about things like games, 3D Graphics and more).
2. Develop in your language of choice (for example .NET or Java).
3. Accelerate hot code portions of ordinary JavaScript apps.
4. In the backend

## Which browsers support WASM today?

Since late 2017, WASM v1 is supported in all modern major browsers (Chrome, Firefox, Safari and Edge)

## What languages are targeted by WASM today?

Almost any language that you think of can target WASM at the moment - they have just got different levels of maturity.

1. C++ is highly mature, because it was used throughout the development of WASM and asm.js.
2. Rust is gaining maturity quite quickly, because the nature of Rust makes it easy to target WASM: Rust’s ownership model is quite compatible with WASM.
3. Java and C# (and JavaScript as well) need a garbage collector and threading.

But WASM doesn’t use a garbage collector, so a common approach is to take a garbage collector and compile it to WASM. You can find C++ garbage collector implementations, and you can compile and ship that as part of your application. That’s going to add extra size, bloat and is pretty inefficient. So At some point in the future, WASM will likely support garbage collection. Maybe: rather than having its own garbage collector, it will interact with the host’s garbage collector.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

And at the moment WASM's threading model is the same as JavaScript's: a single thread of execution. When you invoke a WASM function, your JavaScript virtual machine yields to WASM. So you won’t have JavaScript and WASM running in parallel. You can have web workers, just like you can in JavaScript, so you can parallelise like that.

## 1 and 2: toolchain

### x to wasm

WASM is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

- Write native code: C, C++ or Rust
- Compile it to a wasm module ; currently LLVM targets work best. The compiler tool chain that currently has the most support for WebAssembly is called LLVM. There are a number of different front-ends and back-ends that can be plugged into LLVM.

Once the module is fetched, it will be compiled at runtime.

Sources: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

NB:
Most WebAssembly module developers will code in languages like C and Rust and then compile to WebAssembly, but there are other ways to create a WebAssembly module. For example, there is an experimental tool that helps you build a WebAssembly module using TypeScript, or you can code in the text representation of WebAssembly directly.

## 3 JS to WASM

## 4

TBD

## Zoom: WASM in the web

### Why WASM is faster than JS

Fast to load (= fast to transport the compiled file over the network)
and parse
and execute (e.g. wasm can convert a + into a single cpu instruction)

The advantage of WASM is that it is a much lower level representation of the program than the equivalent JavaScript. This makes it possible for the engine to run the code much faster than the more sophisticated and expressive JavaScript. The limited range of expression that WASM allows probably means that you aren't going to be writing directly to it. Instead the idea is that a compiler will produce WASM from other langauges.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

### How the browser deals with WASM modules / how WASM runs on the web

// todo
What an engine does: actually, an engine is more than just a compiler.
With JS code:
With webassembly code:...
// todo

Imagine we're creating a WASM module that just adds a couple of numbers together:

- Build
- write it in a high level language (rust or C++)
- take a toolchain for that language to compile it into a wasm binary.
- Run

* Because The wasm binary itself has sections within it that export and import functions (similar to JavaScript modules, which export and import functions): the JS code will load up the wasm code, and you’ll be able to see it and invoke it from JavaScript.
* Under the hood, rather than that function being interpreted as JavaScript code, that function will be running in the web assembly virtual machine.

That’s how you currently load wasm modules through JavaScript to invoke compiled code.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

---
