## What is the core problem that web assembly is trying to solve?

respond to real engineering problems that we’ve had with ASM.js. Loading a big game from Epic or Unity can take 20 - 30 seconds. That’s too long. With a compressed abstract syntax tree encoding that’s 20 times faster, just a couple seconds, that’s what you want. So there’s a real reason for wasm, and it is a valid reason.

5:45 Personally, when I look at the way we run applications in the web at the moment, I think they are incredibly inefficient and convoluted.
6:00 JavaScript used Babel or TypeScript, to create a modern typed language around JavaScript.
6:10 We have complicated and advanced build tools that do things like tree shaping, minification, transpiling and so on - it can be quite obscure.
6:25 To pass that code to the browser, it’s only option is to transpile it down to one of the more basic JavaScript versions and send it as text.
6:35 It’s pretty inefficient.
6:40 The browser then has to parse the text into an Abstract Syntax Tree, then run it in an interpreter, then move it through various different optimisation levels so that your code gets faster.
6:50 On the development side, we’ve got some advanced tooling.
6:55 On the browser, we’ve got an advanced runtime with multiple levels of optimisation.
7:00 In the middle, we’ve got a horrible mechanism by where we’re delivering it in a basic and very inefficient text format, because that’s the way the web was designed.
7:15 The impact of the bottleneck is twofold; one is the time it takes to deliver that to the browser, and the other is the overall performance and the time it takes to warm up the JavaScript code to run quickly within the browser.
7:30 Ignoring the fact that web assembly brings different languages to the web, JavaScript itself is pretty inefficiently executed.
7:40 Web assembly in simple terms solves that problem.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

BUT ALSO: beyond WASM:

## What is WASM

WASM is an efficient, low-level assembly-like language / bytecode.

Core features:

- performant // near-native-speed
- portable // it's a compilation target
- safe // no memory overflow

It **runs in all modern browsers**.

It's also...:

- a shortcut to your JS engine's optimizer

- a secure, safe, fast runtime that you can target with a wide range of languages.

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

## Where does it come from

See chapter on ASM+PNaCl

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

## Where does WASM come from

## Why it will change the world / Benefits

- Faster web applications
- Developer experience: no more tower of Babel
- Web dev accessible to all developers
- Help JS win: shared array buffer extension, eventually all the browsers and webviews will support wasm syntax to serve the compile target master and free JavaScript so it can serve the JavaScript master.
- Laboratory for the future of the web
- Remember that JS will evolve, too: SIMD, ...
- wasm will grow to include lots and lots of expressiveness for lots and lots of languages, JS included. 


https://zendev.com/2018/06/26/webassembly-accelerating-future-web-development.html



## Warning

WASM is still early stage. no native strings, no exception handling and so on. These things can be emulated within the basic WASM but the resulting code tends to be slow. The next step is for a W3C working group to be formed to complete the formal specification.

https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html feb 2017

## WASM use cases

- heavily CPU-bound number computations e.g. games (via opengl)
- you'll be consuming compiled binaries
- Deliver existing C/C++ applications over the web (Talking about things like games, 3D Graphics and more).
- Develop in your language of choice (for example .NET or Java).
- Accelerate hot code portions of ordinary JavaScript apps.

Src: https://www.inovex.de/blog/webassembly-production/

## Brief History of WASM

WASM is an MVP. Currently, WASM 1.0 has shipped in 4 major browser engines. 
2015: WASM community group
2017: cross browser consensus
2018: draft of the specification 1.0: WASM core spec (=syntax, naming, building, validayion, execution + the standard for the binary format ie types and values), WASM JS interface (interactions between WASM modules and JS, data storage, sandboxing), WASM web API (rules about module compilation and interactions between the dom and the WASM modules)

ASM paved the way to WASM.

## Challenges & future of WASM

### Challenges today

WASM only has four types at the moment; they’re all numeric (two integer types and two floating point types).
So: implementing a WASM function that adds two numbers is fairly trivial; but Strings are more difficult.
One way to handle string data at the moment is to use linear memory; it has memory that you can read and write to from WASM and JavaScript.
The interesting thing here is to model strings, you share the same piece of memory with null-terminated data.
Real hello world application would look a bit complicated and slightly strange, which is why people who use it use a high-level toolchain
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

Challenge at the moment: there’s quite a lot of complexity involved in interfacing between JavaScript and web assembly. Calling functions is really easy - you can send stuff backwards and forwards, but it’s the types that you’re sending back and forth that is the challenge.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

Next challenges:

- Security

### Future

#### Near

Features planned for WASM 2.0:  
* multi-threading model and garbage collection // C# and Java support will become possible
* multi-value returns
* host binding (it will be easier to expose JavaScript objects to WASM) 

#### Distant  
 
https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723

Once all the browsers support both WASM and ASM.js, then WASM can start to grow extra semantics that need not be put into JS.
They may in fact be put into both JavaScript and WASM because it’s the same one engine (1vm). But there are certain things we might not want to ever put into JS that could be put into WASM:
- shared memory array buffers to get multi-threaded games. Too complicated for JS: risk for race conditions in JavaScript, fragile process with bug hazards
- zero cost exceptions might not make sense in JavaScript. They require some compiler and runtime cleverness, but they do make sense for C++, and Swift. Might benefit other languages like C++ or Haskell
- call/cc (call-with-current-continuation). Call/cc is too powerful a tool. It has challenges for JS engines in implementation and security hazards. You have these non-local functional gotos. You can call a continuation and be off in a different stack. So it’s not like the local, limited continuations like we have in generators in ES6. It’s a deeper continuation. So call/cc could be put into wasm, into the engine that handles both wasm and JavaScript down the road.



