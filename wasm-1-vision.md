## WASM: origins 

What is the core problem that WASM is trying to solve?   

* Web apps are slow and complicated - it takes to deliver JS to the browser (because JS is sent in a non-compact text format), and it takes time + it is complicated to execute it (to warm up the JS code to run quickly within the browser). We end up with: on the one hand, a complicated dev toolchain to reduce the payloads sent to the browser (think Babel, minification, tree shaking, minification, transpiling etc.) ; on the other hand, an advanced runtime with multiple levels of optimisation (JIT compilers and optimizers do a great job but the whole JS running path is still slow complicated). Projects such as ASM.js took a stab at it, but loading large ASM.js resources was still slow (+ ASM was not universally implemented).
* Browsers so far could only be targeted with one single language: JS. 

WASM to the rescue: 
* WASM has a compressed Abstract Syntax Tree encoding that’s 20 times faster. 
* WASM is a compilation target.   

Additionally:   
Because WASM is a compilation target, its impact will ripple to other languages too.   
More on that later. 


_Do we really need yet another tool? Yet another language? Aren't we of finally having a break from frontend fatigue, with webpack + Angular or React?_
Well, exactly - WASM aims at relieving some of the the reasons why web dev tooling is complicated and evolving so fast. But it can also do much more - WASM is a vision for the future of the web, and of programming in general.

## Brief timeline of WASM 

Projects such as ASM.js and PINCl have paved the way to WASM. 
WASM is an MVP. Currently, WASM 1.0 has shipped in 4 major browser engines.  
* 2015: WASM community group
* 2017: cross browser consensus
* 2018: draft of the specification 1.0: WASM core spec (=syntax, naming, building, validayion, execution + the standard for the binary format ie types and values), WASM JS interface (interactions between WASM modules and JS, data storage, sandboxing), WASM web API (rules about module compilation and interactions between the dom and the WASM modules).

## So: What is WASM?

WASM is an efficient, low-level assembly-like language / bytecode.

Core features:
- performant // it runs at near-native-speed
- portable // it's a compilation target
- safe // no memory overflow

It: 
* **runs in all modern browsers**. 
* can be targeted with a wide range of languages

It's also...:

- a shortcut to the JS engine's optimizer

- a compilation target for low-level code (e.g. C, C++), and has bindings that enable that code to access the capabilities of the browser.

- a web standard that defines a binary format, and a corresponding assembly-like text format for executable code in web pages

- interactive apps in the browser depend on the JS VM, which runs the JS language. That's how it's been. WASM brings in another virtual machine, another runtime. But contrary to JS that is rather high-level, wasm is much more low-level.

- a new low-level language that runs in the browser.

wasm is PORTABLE, size and loadtime-efficient format suitable for compilation to the web (and others).
It's a low-level assembly-like language, that runs in modern browsers at near-native perf.

It's not a binary blob launched in your browser ; it's a human-readable code bytecode that is compiled at runtime.

source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

WebAssembly (WASM) is a low-level intermediate language that can be processed by the JavaScript engine alongside JavaScript.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

WebAssembly is really the first W3C based open standard for running native code in the browser, and they recently standardized their support for threading.

WebAssembly brings another kind of virtual machine to the browser that is a much more low-level language.
One of the goals of WebAssembly is to make a new assembly language that is a compilation target for a wide range of other languages such as C++, Java, C# and Rust. C++ is highly mature, Rust is maturing rapidly. Java and C# are a little further behind because of the lack of garbage collection support in WebAssembly. At some point in the future WebAssembly will have it’s own garbage collection perhaps by using the Javascript garbage collector.
At runtime you use JavaScript to invoke functions that are exported by your WebAssembly instance. It should be noted that at the moment there is quite a lot of complexity involved in interfacing between WebAssembly and JavaScript. A lot of this complexity comes from the type system.
WebAssembly is still a very young technology. Future plans include threading support, garbage collection support, multiple value returns.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Why can it run anywhere? / Why is it so portable?

WASM could be used as a portable binary format on many platforms, bringing great benefits in portability, tooling and language-agnosticity.

https://webassembly.org/docs/non-web/

Because:

- it runs on the web (JS VM supports WASM), which is on a lot of platform
- Non-Web environments may include JavaScript VMs (e.g. node.js), however WebAssembly is also being designed to be capable of being executed without a JavaScript VM present.
  - the plan is to keep non-Web path such that it doesn’t require Web APIs (the core features will be within wasm itself: certain features that are core to WASM semantics that are similar to functions found in native libc would be part of the core WASM spec as primitive operators)
  - because it's closer to machine language (it supports C/C++ level semantics), VMs are easier to implement on multiple platforms
  - There is even a project for a cross-platform WASM virtual machine: Life is written in Go, built for running computationally heavy code on practically any device you can imagine.

e.g. on servers in datacenters, on IoT devices, or mobile/desktop apps, or even embedded within larger programs.

## Why it will change the world? / Benefits

1) WASM will accelerate the future of web development  
* New performance-demanding use cases become accessible to the web
* New libraries become accessible to the web
* WASM breaks down the JS monopoly... 
WASM enables linguistic diversity will ; this will dramatically diversify the languages available for building front-end applications and tools. Web development will become accessible to developers coming from other languages ; JS developers will benefit from their experience, and inversely.
* ... and helps JS win   
WASM will grow to include lots and lots of expressiveness for lots and lots of languages, JS included. 
With shared array buffer extension, eventually all the browsers and webviews will support WASM syntax to serve the compile target master, and free JS so it can serve the JS master.
* WASM can be used as a laboratory for the future of the web

2) UX: WASM will make (the web) faster
WebAssembly Will Enable Parallelism 
https://zendev.com/2018/06/26/webassembly-accelerating-future-web-development.html  

3) WASM will smooth DevX
Not just on the web! Languages interop is complicated, and WASM can help.  
Developer experience: no more tower of Babel

4) More


## Warning

WASM is still early stage. No native strings, no exception handling and so on. These things can be emulated within the basic WASM but the resulting code tends to be slow. The next step is for a W3C working group to be formed to complete the formal specification.

https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html 

## WASM use cases

- web: heavily CPU-bound number computations e.g. games (via opengl)
- web: Deliver existing C/C++/... applications over the web (Talking about things like games, 3D Graphics and more) 
- web: Accelerate hot code portions of ordinary JavaScript apps 
- web/others: you'll be consuming compiled binaries
- web/others: Develop in your language of choice (for example .NET or Java).

## Future of WASM

### Future

#### Near

Features planned for WASM 2.0:  
* multi-threading model and garbage collection // C# and Java support will become easier
* multi-value returns
* host binding // JS objects will be more easily exposed to WASM 

#### Distant  
 
https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723

Once all the browsers support both WASM and ASM.js, then WASM can start to grow extra semantics that need not be put into JS.
They may in fact be put into both JavaScript and WASM because it’s the same one engine (1vm). But there are certain things we might not want to ever put into JS that could be put into WASM:
- shared memory array buffers to get multi-threaded games. Too complicated for JS: risk for race conditions in JavaScript, fragile process with bug hazards
- zero cost exceptions might not make sense in JavaScript. They require some compiler and runtime cleverness, but they do make sense for C++, and Swift. Might benefit other languages like C++ or Haskell
- call/cc (call-with-current-continuation). Call/cc is too powerful a tool. It has challenges for JS engines in implementation and security hazards. You have these non-local functional gotos. You can call a continuation and be off in a different stack. So it’s not like the local, limited continuations like we have in generators in ES6. It’s a deeper continuation. So call/cc could be put into wasm, into the engine that handles both wasm and JavaScript down the road. 

### Challenges today

* Interop between for example JS and WASM is still complex: calling functions is really easy - you can send stuff backwards and forwards, but it’s the types that you’re sending back and forth that is the challenge 
* See planned features



