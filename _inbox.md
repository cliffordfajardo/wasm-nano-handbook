---

Myth debunking suit: on.
No hard feelings, healthy skeptiscism is healthy.

It's not just a tool, it will change HOW

A matter of scale
and scale
, when you could instead go on and learn about React hook

<!-- 2. A matter of scale -->

Understand Wasm is not a new framework. It's a whole new universe. Don;t get fooled "it's super new"... "just an MVP"
and it will influence how we build for the web

<!-- , why should I learn about it, "I've just gotten along with React hooks and my inbox is flooded with web news". -->

Well, I've heard about it but that's only for games, right?

<!-- which you could hesitate to learn because it's just hype.
It's an actual new tool that's embedded in browsers.
It's as serious as the new ES6 syntax was, or as any cross-browser feature. -->

Why should you, a honest web developer who's solid on her tools, care about WebAssembly?
One more

If you're reading this, you might

Wasm is not just for games
Things will be fine

### tbd

Is there a fully-fledged non-JS framework?
Maybe, but won't make sense just yet - even though some bindings are in-place, JS is still best for DOM manipulation and others.

it will be compiled at runtime

Compiler toolchains:

Rust to Wasm:

C or C++ to Wasm:

C --> LLVM IR // clang  
LLVM IR --> Wasm // LLVM Wasm was backend or Emscripten using asm2wasm

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

- Web apps are slow and complicated - it takes to deliver JS to the browser (because JS is sent in a non-compact text format), and it takes time + it is complicated to execute it (to warm up the JS code to run quickly within the browser). We end up with: on the one hand, a complicated dev toolchain to reduce the payloads sent to the browser (think Babel, minification, tree shaking, minification, transpiling etc.) ; on the other hand, an advanced runtime with multiple levels of optimisation (JIT compilers and optimizers do a great job but the whole JS running path is still slow complicated). Projects such as ASM.js took a stab at it, but loading large ASM.js resources was still slow (+ ASM was not universally implemented).

Wasm to the rescue:

- It has a compressed Abstract Syntax Tree encoding that’s 20 times faster.
- It is a compilation target

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

---
