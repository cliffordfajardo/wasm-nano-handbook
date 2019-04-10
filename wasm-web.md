# Wasm for the web // 🚧WIP

_On how Wasm runs in the environment that gave life to it._  
_↠ Up Next: [Ecosystem and Resources](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-ecosystem-and-resources.md)_

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/web.jpg">   
  	<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

[1. Wasm, JS, and the browser(s)](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md#wasm-js-and-the-browsers)  
[2. Wasm is fast, Wasm is fast](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md#wasm-is-fast-wasm-is-fast)  
[3. Under the hood](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md#under-the-hood)  
[4. Recent V8 improvements](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md#recent-v8-improvements)  
[5. Tools for web developers](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md#tools-for-web-developers)

_Before digging into this chapter: if you're a bit rusty on the basics of browsers engines, check out (TBD add link)._

---

## Wasm, JS, and the browser(s)

Before we dig deeper into the details of how browsers run Wasm, let's clarify:

- **Wasm won't replace JS**. You might have read that Wasm will instead _complement_ JS.  
  In fact, we can even go one step further and say that Wasm will push JS forward.  
  TBD explain.
- Wasm (v1) is supported in **all modern major browsers**: Chrome, Firefox, Safari and Edge.

## Wasm is fast, Wasm is fast

TBD add sources

### A grain of salt

- Performance issues are often rather caused by rendering/paint; see Google devs article
- GC adds overhead; see wasmer podcast

### A brief history of JS performance in the browser

- JS was created in 1995; it was interpreted, so running slow.
- In 2008, the performance war started, leading to JIT (just in time compilers). They lead to a manyfold perf improvement: JS was running 10 times faster. JIT compilers make JS run faster, by monitoring it as it's running and sending hot code paths to be optimized. Also, the JIT has added some overhead runtime: optim+deoptim, plus memory (e.g. to store baseline and optimized version of a function).

Source: hacks.mozilla.org

#### Where we are with Wasm: short version

Today with JS, the engine must do on the main thread:  
Parse → Compile+Optimize → Re-optimize → Execute → Garbage Collection.

With Wasm:  
Decode → Compile+Optimize → Execute.

#### Where we are with Wasm: detailed version

Step -1:  
Fetching Wasm is faster (less network bandwith because Wasm files are more compact than JS even compressed).

Parse/Decode:

- The browser must parse JS into an Abstract Syntax Tree then converted into an Immediate Representation (bytecode).
- Wasm syntax is already an IR/AST.

Compile+optimize:

- JS: with JIT, JS is compiled _during_ execution.
- Wasm:

  - already optimized via LLVM (AOT=ahead-of-time)
  - No need to run observation rounds for types since it's already typed
  - No need to compile different versions of the code depending on the observed types
  - streaming compilation (newer)

Reoptimize:

- JS: 2 costs: 1)throw out the optimized version and fallback to baseline version, 2) reoptimization
- Wasm: no need to deoptimize ; it's predicatble thanks to types.

Execute:

- JS: can run efficiently when properly optimized ; but most devs don't know about JIT internals / focus on code readability.
- Wasm: executes faster because is better optimized.

GC:

- JS: GC takes time ; it's well planned by now but still is an overhead!!
- Wasm: doesn't have GC since memory is manually managed.

## Under the hood

### How the browser deals with WASM modules / how WASM runs on the web

- Wasm is shipped as a module (`.wasm`) (tbd link to section on modules). Just like a JS module, it has sections within it that export and import functions.
- The Wasm module can be loaded in JS, and the Wasm code can be invoked from JS.
- Under the hood, rather than that function being interpreted as JS code, that function will be running in the Wasm virtual machine ; i.e. will be compiled at runtime.
- You can debug wasm directly

Note that it’s the same one engine ("1vm") that deals with wasm and JS (Brendan Eich).

### JS <-> Wasm interop

- At the moment, Wasm can only use numbers (int and floating points) as params and return values
- To deal with strings, one must use Wasm's Memory API. which is a way for Wasm and JS to share memory.
- wasm-bindgen: TBD

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

#### JS Wasm API // TBD

- Module
- Memory
- Table
- Instance

TBD: https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts#WebAssembly_key_concepts  
TBD schema

#### How memory works: with code examples // TBD

#### How module loading works: with code examples // TBD

compare a rust-built project with webpack with manual loading

## Recent V8 and SpiderMonkey improvements

V8, 2018:

- debug: source maps
- run faster:
  - streaming compilation: start compiling before the module has finished downloading
  - Liftoff: V8's team built a new compiler called Liftoff. Lift off immediately executes the Wasm bytecode ; in the meantime, Turbofan (the optimizing compiler) optimizes the modules, off the main thread. When Turbofan is done, the module is hot swapped.
  - ++++ threads: bring pthread (C++) and others to the web for true parallelism // Danilo "Use the platform"

Also Next browser features:

- Direct DOM calls
- Shared memory between threads
- SIMD
- Exceptions
- Garbage collection
- ES6 module integration
- Dev tools

src mozilla

## Tools for web developers

- AssemblyScript
- The explorer
- See toolchain chapter
- hasher parcel repo
