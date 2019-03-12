## Wasm: origins 

The web is great.
JS is great.  

But it's not perfect. 

Building and running web apps but limits:

* Browsersso far could only be targeted with one single language: one of the most ubiquitous piece of sugars JS.
* Loading and executing JS is still slower than native code Anita is Copy intensives on mobile. 

Previous attempts to solve one or the other have met a mitigated success: no consitent performance gain and, not crossrowsers.
Wasm is the result of a concerted approach to solve these, based on the learnings of these previous approaches.

So, Wam is born for the web.  
But:  beacuse it's also a compilatiin target (more on ghat later), its impact go wag beyond it.


* Web apps are slow and complicated - it takes to deliver JS to the browser (because JS is sent in a non-compact text format), and it takes time + it is complicated to execute it (to warm up the JS code to run quickly within the browser). We end up with: on the one hand, a complicated dev toolchain to reduce the payloads sent to the browser (think Babel, minification, tree shaking, minification, transpiling etc.) ; on the other hand, an advanced runtime with multiple levels of optimisation (JIT compilers and optimizers do a great job but the whole JS running path is still slow complicated). Projects such as ASM.js took a stab at it, but loading large ASM.js resources was still slow (+ ASM was not universally implemented). 

Wasm to the rescue: 
* It has a compressed Abstract Syntax Tree encoding that’s 20 times faster. 
* It is a compilation target    

Additionally:   
Because Wasm is a compilation target, its impact will ripple to other languages too.   

_Do we really need yet another tool? Yet another language? Aren't we of finally having a break from frontend fatigue, with webpack + Angular or React?_
Well, exactly - Wasm aims at relieving some of the the reasons why web dev tooling is complicated and evolving so fast. But it can also do much more - Wasm is a vision for the future ofhe web, and of programming in general.

## So: What is Wasm?

**Wasm is an efficient, low-level assembly-like language / bytecode,** that runs on all modern browsers (1) (2) at near-native speed and (3) that is a compilation target for a wide range of other languages.


Core features:
- performant // it runs at near-native-speed, in a way it's a shortcut to the JS engine's optimizer
- **runs in all modern browsers**. 
- portable // it's a compilation target for a wide range of other languages such as C++ and Rust
- safe // no memory overflow 
- standardized // there's consensus around it

Plus: 
- has bindings that enable that code to access the capabilities of the browser / of JS

## Why can it run anywhere? / Why is it so portable?

Wasm could be used as a portable binary format on many platforms, bringing great benefits in portability, tooling and language-agnosticity.

https://webassembly.org/docs/non-web/

Because:

- it runs on the web (JS VM supports Wasm), which is on a lot of platforms 
- Non-Web environments may include JavaScript VMs (e.g. node.js), however WebAssembly is also being designed to be capable of being executed without a JavaScript VM present. 
-  it takes advantage of common hardware capabilities available on a wide range of platforms, including mobile and IoT.
 - the plan is to keep non-Web path such that it doesn’t require Web APIs (the core features will be within Wasm itself: certain features that are core to Wasm semantics that are similar to functions found in native libc would be part of the core Wasm spec as primitive operators)
 - because it's closer to machine language (it supports C/C++ level semantics), VMs are easier to implement on multiple platforms
 - There is even a project for a cross-platform Wasm virtual machine: Life is written in Go, built for running computationally heavy code on practically any device you can imagine. 
- its AMI is platform-agnostic: 
WebAssembly does not specify any APIs or syscalls, only an import mechanism where the set of available imports is defined by the host environment. In a Web environment, functionality is accessed through the Web APIs defined by the Web Platform. Non-Web environments can choose to implement standard Web APIs, standard non-Web APIs (e.g. POSIX), or invent their own.

e.g. on servers in datacenters, on IoT devices, or mobile/desktop apps, or even embedded within larger programs. 



## Why it will change the world? / Benefits

1) Wasm will accelerate the future of web development  
* New performance-demanding use cases become accessible to the web
* New libraries become accessible to the web
* Wasm breaks down the JS monopoly... 
Wasm enables linguistic diversity ; this will dramatically diversify the languages available for building front-end applications and tools. Web development will become accessible to developers coming from other languages ; JS developers will benefit from their experience, and inversely.
* ... and helps JS win   
Wasm will grow to include lots and lots of expressiveness for lots and lots of languages, JS included. 
With shared array buffer extension, eventually all the browsers and webviews will support Wasm syntax to serve the compile target master, and free JS so it can serve the JS master.
* Wasm can be used as a laboratory for the future of the web

2) UX: Wasm will make (the web) faster
WebAssembly Will Enable Parallelism 
https://zendev.com/2018/06/26/webassembly-accelerating-future-web-development.html  

3) DevX: Wasm could make our lives easie
Not just on the web! Languages interop is complicated, and Wasm can help.  
Developer experience: no more tower of Babel

4) More

## Wasm use cases

- web: heavily CPU-bound number computations e.g. games (via opengl)
- web: Deliver existing C/C++/... applications over the web (Talking about things like games, 3D Graphics and more) 
- web: Accelerate hot code portions of ordinary JavaScript apps 
- web/others: you'll be consuming compiled binaries
- web/others: Develop in your language of choice (for example .NET or Java).

## Past of Wasm 

Projects such as ASM.js and PNaCl have paved the way to Wasm.  

* 2015: Wasm community group
* 2017: cross-browser consensus
* 2018: draft of the specification 1.0: core spec (=syntax, naming, building, validayion, execution + the standard for the binary format ie types and values), JS interface (interactions between Wasm modules and JS, data storage, sandboxing), web API (rules about module compilation and interactions between the dom and the Wasm modules).

## Wasm today

* Wasm 1.0 is an MVP, that has shipped in 4 major browser engines. 
* It is still early stage: no native strings nor exception handling ; these can be emulated within the basic Wasm but the resulting code is slow. Also, interop between for example JS and Wasm is still complex (calling functions is easy, but it’s the types to send back and forth that is the challenge)
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html 

## Future of Wasm

### Future

#### Near

Features planned for Wasm 2.0:  
* multi-threading model and garbage collection // C# and Java support will become easier
* multi-value returns
* host binding // JS objects will be more easily exposed to Wasm 

#### Distant  
 
https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723

Once all the browsers support both Wasm and ASM.js, then Wasm can start to grow extra semantics that need not be put into JS.
They may in fact be put into both JavaScript and Wasm because it’s the same one engine (1vm). But there are certain things we might not want to ever put into JS that could be put into Wasm:
- shared memory array buffers to get multi-threaded games. Too complicated for JS: risk for race conditions in JavaScript, fragile process with bug hazards
- zero cost exceptions might not make sense in JavaScript. They require some compiler and runtime cleverness, but they do make sense for C++, and Swift. Might benefit other languages like C++ or Haskell
- call/cc (call-with-current-continuation). Call/cc is too powerful a tool. It has challenges for JS engines in implementation and security hazards. You have these non-local functional gotos. You can call a continuation and be off in a different stack. So it’s not like the local, limited continuations like we have in generators in ES6. It’s a deeper continuation. So call/cc could be put into Wasm, into the engine that handles both Wasm and JavaScript down the road. 



