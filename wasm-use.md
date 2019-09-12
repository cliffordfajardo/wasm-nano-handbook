# Use case and usage modes today - from a developer's perspective // 🚧WIP

_On how you can use Wasm today, depending on your context._  
 _↠ Up Next: [Wasm for the Web](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-web.md)_

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/use.jpg">   
 	<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

// todo why: when would you use it
[1. Usage modes](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-use.md#usage-modes)  
[2. Toolchains](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-use.md#toolchains)  
[3. Mapping: usage modes to toolchains](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-use.md#mapping-usage-modes-to-toolchains)  
[4. A note on dev teams](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-use.md#a-note-on-dev-teams)

---

## ⚡ TL;DR

You can use WebAssembly today.  
You typically wouldn't write it directly ; instead you would write it another language and then compile this code down to Wasm. Rust and C++ are best supported for now, but alternatives such as AssemblyScript are also available.


## Why?


## Usage modes

1. Use as dependency
2. Accelerate hot code portions of ordinary JS apps
3. Develop for the web in the developers' language of choice
4. Deliver existing applications over the web, such as games / 3D Graphics
5. Others: see wasmer with docker use case + iOT // TBD

## How does it run, How does memory work?

## Interop

### How Wasm calls x

Wasm doesn’t have any built­in knowledge of JS ; it has a general way to import functions that can accept either JS or Wasm functions.

## Debug

## Toolchains

Because Wasm is an assembly-like format, it's rather hard to write it directly by hand. Usually, you'd write it in another language and compile it to wasm ahead of time.

What languages can you compile down to wasm?
As of today, the support is best for languages which memory is managed - understand "managed manually or semi-manually". That is the case of Rust and C++, for which the toolchains are the most mature.  
But other projects are out there, such as AssemblyScript.

Try them out: https://webassembly.studio/

<p align="center">
<img with="200" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/toolchains-4.jpg"> 
<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

Details: TBD

### C/C++ -> wasm with Emscripten

Emscripten requires JS "glue" code for memory allocation/leaks, etc. About 2000 lines for just a hello world (but this also includes instantiation).

Sources/resources:

- **AssemblyScript**: https://github.com/AssemblyScript/assemblyscript
- https://developers.google.com/web/updates/2018/03/emscripting-a-c-library
- https://developer.mozilla.org/en-US/docs/WebAssembly/Rust_to_wasm

## Mapping: usage modes to toolchains

TBD

## Aside: dev teams

One dot !== one dev, one dot is one _skill unit_ ; e.g. a full-stack dev is one dark grey + one light grey dot.

<p align="center">
<img with="200" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/wasm-use-case.png"> 
<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

### Wasm (Mode 1)

Update your dependencies to replace them by Wasm modules when available.  
In theory if the API doesn't change, there's no work to do on your side. One example of that could be the React team updating their reconciliation algo to use Wasm.  
Benefits:

- A smaller, faster codebase

### Wasm (Mode 2)

Actually rewrite some hot code portions of yours in Wasm.  
Benefits:

- An even smaller, faster codebase
- More dev resources can be allocated to the codebase, and the team can grow heterogeneous, emulating cross-learning.

## trash maybe 🚧WIP

What languages can be compiled to Wasm today?  
Most of them - but with different levels of maturity.  
The ones that are static and LLVM are best supported for now.

- C, C++: highly mature, because it was used throughout the development of WASM and asm.js.
- Rust: gaining maturity rather quickly, because the nature of Rust makes it easy to target Wasm, e.g. Rust’s ownership model
- Java and C# (and JavaScript as well) still need a garbage collector. The way this works today, is that they take compile their GC to Wasm, and ship everything to the app page ; still experimental though.

Alternatively:

- Experimental support:
  - Turboscript
  - TypeScript
  - Walt
- Code in `.wat` directly.

Note: This will evolve. You might be able to write Wasm from TypeScript someday!

### Get started

- C, C++: Emscripten // TBD add links
- Rust: stdweb or bindgen, parcel wasm hasher // TBD add links

## 4

Mostly with C++.

## Get started

- Examples in prod: TBD
- Tutorials: C#, Rust, TBD
- Mode 1: npm packages (+ all the hidden ones)
- Mode 2: TBD. Refer to section 3 to see with languages are supported.

<div align="center"><sub><sup>©maudnals</sup></sub></div>
