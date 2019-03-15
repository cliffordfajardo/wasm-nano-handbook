# Wasm for the web // 🚧WIP    

_On how Wasm runs in the environment that gave life to it._    
_Up Next: [Ecosystem and Resources](https://github.com/maudnals/wasm-nano-handbook/blob/master/5-wasm-ecosystem-and-resources.md)_  


<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/web.jpg">  
</p>  

[1. Wasm, JS, and the browser(s)](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md#wasm-js-and-the-browsers)   
[2. Wasm is fast, Wasm is fast](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md#wasm-is-fast-wasm-is-fast)  
[3. Under the hood](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md#under-the-hood)     
[4. Recent V8 improvements](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md#recent-v8-improvements)   
[5. Tools for web developers](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md#tools-for-web-developers)   


_Before digging into this chapter: if you're a bit rusty on the basics of browers engine, check out (TBD add link)._ 

----

## Wasm, JS, and the browser(s)   

Before we dig deeper into the details of how browsers run Wasm, let's clarify:
* Wasm won't replace JS. You might have read that Wasm will instead _complement_ JS.    
In fact, we can even go one step further and say that Wasm will push JS forward.   
TBD explain.     
* Wasm (v1) is supported in **all** modern major browsers: Chrome, Firefox, Safari and Edge.

## Wasm is fast, Wasm is fast

TBD add sources

### Disclaimer 
* Performance issues are often rather caused by rendering/paint 
* GC adds overhead; see Google devs article 

### A brief history of JS performance in the browser

* JS was created in 1995 ; it was interpreted, so still slow. 
* In 2008, the performance war started, leading to JIT (just in time compilers). They lead to a manyfold perf improvement: JS was running 10 times faster. JIT compilers make JS run faster, by monitoring it as it's running and sending hot code paths to be optimized. Also, the JIT has added some overhead runtime: optim+deoptim, plus memory (e.g. to store baseline and optimized version of a function).    

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
* The browser must parse JS into an Abstract Syntax Tree then converted into an Immediate Representation (bytecode),  
* Wasm syntax is already an IR/AST.  

Compile+ptimize:  
* JS: with JIT, JS is compiled _during_ execution.  
* Wasm:
  * already optimized via LLVM (AOT=ahead-of-time) 
  * No need to run observation rounds for types since it's already typed
  * No need to compile different versions of the code depending on the observed types 
  * streaming compilation (newer)
  
Reoptimize: 
* JS: 2 costs: 1)throw out the optimized version and fallback to baseline version, 2) reoptimization
* Wasm: no need to deoptimize ; it's predicatble thanks to types.  

Execute:  
* JS: can run efficiently when properly optimized ; but most devs don't know about JIT internals / focus on code readability.
* Wasm: executes faster because is better optimized. 

GC: 
* JS: GC takes time ; it's well planned by now but still is an overhead!! 
* Wasm: doesn't have GC since memory is manually managed.  


## Under the hood 

### How the browser deals with WASM modules / how WASM runs on the web   

* Wasm is shipped as a module (`.wasm`) (tbd link to section on modules). Just like a JS module, it has sections within it that export and import functions.  
* The Wasm module can be loaded in JS, and the Wasm code can be invoked from JS. 
* Under the hood, rather than that function being interpreted as JS code, that function will be running in the Wasm virtual machine ; i.e. will be compiled at runtime.  

Note that it’s the same one engine ("1vm") that deals with wasm and JS (Brendan Eich).

### JS <-> Wasm interop 

* At the moment, Wasm can only use numbers (int and floating points) as params and return values  
* To deal with strings, one must use Wasm's Memory API  ; basically a way for Wasm and JS to share memory.
* wasm-bindgen: TBD

https://www.infoq.com/podcasts/colin-eberhardt-webassembly  


## Recent V8 improvements    

2018:    
- debug: source maps  
- run faster:  
   - streaming compilation: start compiling before the module has finished downloading  
   - Liftoff: V8's team built a new compiler called Liftoff. Lift off immediately executes the Wasm bytecode ; in the meantime, Turbofan (the optimizing compiler) optimizes the modules, off the main thread. When Turbofan is done, the module is hot swapped. 
   - ++++ threads: bring pthread (C++) and others to the web for true parallelism // Danilo "Use the platform"

- streaming compilation 
- liftoff
- webassembly threads
- source maps for wasm

Also Next browser features:  

* Direct DOM calls 
* Shared memory between threads 
* SIMD 
* Exceptions
* Garbage collection  
* ES6 module integration 
* Dev tools  

src mozilla

## Tools for web developers   
* AssemblyScript 
* The explorer
* See toolchain chapter   
* hasher parcel repo

---

### tbd  

Is there a fully-fledged non-JS framework? 
Maybe, but won't make sense just yet - even though some bindings are in-place, JS is still best for DOM manipulation and others. 

it will be compiled at runtime


Compiler toolchains:

Rust to Wasm: 

C or C++ to Wasm: 

C --> LLVM IR // clang   
LLVM IR --> Wasm // LLVM Wasm was backend or Emscripten  using asm2wasm 


it will be compiled at runtime

What about wasm to the target machine's assembly code?  
The browser will take care of that.


## What languages are targeted by WASM today?

Almost any language that you think of can target WASM at the moment - they have just got different levels of maturity.


But WASM doesn’t use a garbage collector, so a common approach is to take a garbage collector and compile it to WASM. You can find C++ garbage collector implementations, and you can compile and ship that as part of your application. That’s going to add extra size, bloat and is pretty inefficient. So At some point in the future, WASM will likely support garbage collection. Maybe: rather than having its own garbage collector, it will interact with the host’s garbage collector.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

And at the moment WASM's threading model is the same as JavaScript's: a single thread of execution. When you invoke a WASM function, your JavaScript virtual machine yields to WASM. So you won’t have JavaScript and WASM running in parallel. You can have web workers, just like you can in JavaScript, so you can parallelise like that.

// wasm can support many compiled languages, certainly the static ones right now — particularly the ones that use LLVM. Microsoft has their own compiler so they’ll be doing wasm from a different compiler framework, but that’s great. The more, the merrier.

Certainly GCC or similar could generate wasm, but I think to get to the dynamic languages, like I mentioned Dart, or Ruby, or Python, even JavaScript — that’s gonna require some extensions that I mentioned earlier, like: garbage collection hooks, JIT support, things like that. Otherwise they just won’t be competitive.

There’s good precedent. The JVM grew over many years, thanks to John Rose grew things like `invokedynamic` and other hooks for just in time compilation optimizations like polymorphic inline caching so the JVM is actually a credible dynamic language platform.

All of these runtimes have become polyglot VMs — JavaScript VMs. Java hasn’t died just because the JVM now supports Clojure, and Scala, and other languages. We’re almost at the second golden age of programming languages, you know, take Rust, Haskell, Idris, and other languages.

The more the merrier, I say. It’s not gonna become the tower of Babel because I think JavaScript will be the lingua franca of the browser, today and tomorrow. If you’re writing front-end code or really anything that’s not on the critical path when you profile.

https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723


WASM is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

- Write native code: C, C++ or Rust
- Compile it to a wasm module ; currently LLVM targets work best. The compiler tool chain that currently has the most support for WebAssembly is called LLVM. There are a number of different front-ends and back-ends that can be plugged into LLVM.
Once the module is fetched, it will be compiled at runtime.
Sources: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

### trash me maybe  


* Web apps are slow and complicated - it takes to deliver JS to the browser (because JS is sent in a non-compact text format), and it takes time + it is complicated to execute it (to warm up the JS code to run quickly within the browser). We end up with: on the one hand, a complicated dev toolchain to reduce the payloads sent to the browser (think Babel, minification, tree shaking, minification, transpiling etc.) ; on the other hand, an advanced runtime with multiple levels of optimisation (JIT compilers and optimizers do a great job but the whole JS running path is still slow complicated). Projects such as ASM.js took a stab at it, but loading large ASM.js resources was still slow (+ ASM was not universally implemented). 

Wasm to the rescue: 
* It has a compressed Abstract Syntax Tree encoding that’s 20 times faster. 
* It is a compilation target    

Additionally:   
Because Wasm is a compilation target, its impact will ripple to other languages too.   

_Do we really need yet another tool? Yet another language? Aren't we of finally having a break from frontend fatigue, with webpack + Angular or React?_
Well, exactly - Wasm aims at relieving some of the the reasons why web dev tooling is complicated and evolving so fast. But it can also do much more - Wasm is a vision for the future ofhe web, and of programming in general. 

loading and executing JS i

The advantage of WASM is that it is a much lower level representation of the program than the equivalent JavaScript. This makes it possible for the engine to run the code much faster than the more sophisticated and expressive JavaScript. The limited range of expression that WASM allows probably means that you aren't going to be writing directly to it. Instead the idea is that a compiler will produce WASM from other langauges.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html





It's also...:
- a web standard that defines a binary format, and a corresponding assembly-like text format for executable code in web pages
- interactive apps in the browser depend on the JS VM, which runs the JS language. That's how it's been. Wasm brings in another virtual machine, another runtime. But contrary to JS that is rather high-level, Wasm is much more low-level.
Wasm is PORTABLE, size and loadtime-efficient format suitable for compilation to the web (and others).

It's not a binary blob launched in your browser ; it's a human-readable code bytecode that is compiled at runtime.
source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

It is processed by the JavaScript engine alongside JavaScript.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html
WebAssembly is really the first W3C based open standard for running native code in the browser, and they recently standardized their support for threading.

WebAssembly brings another kind of virtual machine to the browser that is a much more low-level language.
One of the goals of WebAssembly is to make a new assembly language that is a compilation target for a wide range of other languages such as C++, Java, C# and Rust. C++ is highly mature, Rust is maturing rapidly. Java and C# are a little further behind because of the lack of garbage collection support in WebAssembly. At some point in the future WebAssembly will have it’s own garbage collection perhaps by using the Javascript garbage collector.
At runtime you use JavaScript to invoke functions that are exported by your WebAssembly instance. It should be noted that at the moment there is quite a lot of complexity involved in interfacing between WebAssembly and JavaScript. A lot of this complexity comes from the type system.
WebAssembly is still a very young technology. Future plans include threading support, garbage collection support, multiple value returns.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly 

// todo
What an engine does: actually, an engine is more than just a compiler.
What it does:
With JS code:
With webassembly code:...
// todo
Imagine we're creating a WASM module that just adds a couple of numbers together:

- Build
- write it in a high level language (rust or C++)
- take a toolchain for that language to compile it into a wasm binary.
- Run
----
