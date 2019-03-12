### Assembly 
Machine has: 
* CPU: registers (short term memory) + ALU (arithmetic logic unit) 
* RAM

## Why WASM is faster than JS  

* JS was created in 1995 ; it was interpreted, so still slow. 
* In 2008, the performance war started, leading to JIT (just in time compilers). They lead to a manyfold perf improvement: JS was running 10 times faster. JIT compilers make JS run faster, by monitoring it as it's running and sending hot code paths to be optimized. Also, the JIT has added some overhead runtime: optim+deoptim, plus memory (e.g. to store baseline and optimized version of a function).   


Source: hacks.mozilla.org


6:40 The browser then has to parse the text into an Abstract Syntax Tree, then run it in an interpreter, then move it through various different optimisation levels so that your code gets faster. 
WASM syntax is already an AST.
Sources: https://www.infoq.com/podcasts/colin-eberhardt-webassembly



Fast to load (= fast to transport the compiled file over the network)
and parse
and execute (e.g. wasm can convert a + into a single cpu instruction)

The advantage of WASM is that it is a much lower level representation of the program than the equivalent JavaScript. This makes it possible for the engine to run the code much faster than the more sophisticated and expressive JavaScript. The limited range of expression that WASM allows probably means that you aren't going to be writing directly to it. Instead the idea is that a compiler will produce WASM from other langauges.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

### How the browser deals with WASM modules / how WASM runs on the web

it’s the same one engine (1vm) that deals with wasm and JS.

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




## Which browsers support WASM today?

Since late 2017, WASM v1 is supported in all modern major browsers (Chrome, Firefox, Safari and Edge)



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
