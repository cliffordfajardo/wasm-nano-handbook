## What is the core problem that web assembly is trying to solve?

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

## Why can it run anywhere?

"run anywhere" because:

- the web has a VM
- it's closer to machine language, so VMs are easier to implement. And there is even a project for a cross-platform WebAssembly virtual machine: Life is written in Go, built for running computationally heavy code on practically any device you can imagine.

## Why it will change the world / Benefits

- Faster web applications
- Developer experience: no more tower of Babel
- Web dev accessible to all developers

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

## History and group

WASM is an MVP
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

### Future

Currently: WebAssembly 1.0 has shipped in 4 major browser engines.

WASM 2.0: multi-threading model and garbage collection (C# and Java), multi-value returns, host binding (it will be easier to expose JavaScript objects to WASM), Integrating WASM modules with JavaScript modules.

webpack support would be awesome: rust-loader, cpp-loader

Q: where is the direct access to web apis?

WASM has the power of:

- Breaking down the monopoly. The web is the most ubiquitous platform that we have at the moment, and it’s quite bad that we only have one language that has first class support. The web will open up to many other developers like C#, Java... !
- Existing web developers, who are comfortable with JavaScript or TypeScript, will start looking at the performance benefits of WASM, and they’ll want to be part of it too.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly
