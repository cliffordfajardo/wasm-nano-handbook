# # 1 Back to basics

q?

binary vs bytecode

are js and wasm using the same vm?

# What is WASM

## Where it comes from

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

## How to write WASM

WASM is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

Write native code (C, C++ or webGL) and compile it to a wasm module (LLVM target).

Once the module is fetched , it will be compiled at runtime.
source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

Details:
The compiler tool chain that currently has the most support for WebAssembly is called LLVM. There are a number of different front-ends and back-ends that can be plugged into LLVM.

NB:
Most WebAssembly module developers will code in languages like C and Rust and then compile to WebAssembly, but there are other ways to create a WebAssembly module. For example, there is an experimental tool that helps you build a WebAssembly module using TypeScript, or you can code in the text representation of WebAssembly directly.

## How it works

## Why it will change the world / Benefits

- Faster web applications
- Developer experience: no more tower of Babel
- Web dev accessible to all developers

## Why WASM is faster in the web

Fast to load (= fast to transport the compiled file over the network)
and parse
and execute

The advantage of WASM is that it is a much lower level representation of the program than the equivalent JavaScript. This makes it possible for the engine to run the code much faster than the more sophisticated and expressive JavaScript. The limited range of expression that WASM allows probably means that you aren't going to be writing directly to it. Instead the idea is that a compiler will produce WASM from other langauges.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

## Warning

WASM is still early stage. no native strings, no exception handling and so on. These things can be emulated within the basic WASM but the resulting code tends to be slow. The next step is for a W3C working group to be formed to complete the formal specification.

https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html feb 2017

## WASM language

It's a STACK MACHINE language.

A stack is a data structure that has two operations: push and pop. It's LIFO order (last in first out).
A stack machine is a stack for which items are instructions, which run and evaluate, and push and pop values on this stack.

WebAssembly only supports 4 types - 2 integer types and 2 floating point types. To model strings you share the same piece of linear memory - memory that can read from and write to from both WebAssembly and JavaScript.

Stack is a LIFO data structure that has 2 operations: push things onto the stack, or pop them off the stack.
e.g.: a call stack

Src: https://www.youtube.com/watch?v=6Y3W94_8scw Demystifying web assembly

## WASM flavors / representations

which one is the assembly?

Binary opcode:
0x6a (= add operation)

(Stack representation:
Just for us to understand

```
i32.const 1
i32.const 2
i32.add
call $log
```

"add 1 to the stack, add 2 to the stack, call add (add takes 2 args, by just popping them off the stack), push the result on the stack"

)

AST (abstract syntax tree) representation (= s-expressions), more human-readable:

```
(call $log
	(i32.add
		(i32.const 1)
		(i32.const 2)
	)
)
```

Src: https://www.youtube.com/watch?v=6Y3W94_8scw

text representation:

If you’re writing code to run directly on a microprocessor, the instruction that the processor understands is a low-level machine code; bytes and so on.
3:06 Most assembly languages will have a slightly more readable version - the assembly language. You’ll have opcodes being represented as mnemonics instead of bytes. So the text format you see for WASM is just a more human version of the binary format which is the underlying WASM itself. It’s a very light syntactic sugar - there’s almost a 1-1 mapping between the text format and the binary format.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

```javascript
(local i32 i64)
  get_global 0
  i32.const 96
  i32.sub
  tee_local 2
  set_global 0
  get_local 2
  i32.const 8
  i32.add
  i32.const 16
  i32.add
```

## What languages are targeted by WASM today?

Almost any language that you think of can target WASM at the moment - they have just got different levels of maturity.

1. C++ is highly mature, because it was used throughout the development of WASM and asm.js.
2. Rust is gaining maturity quite quickly, because the nature of Rust makes it easy to target WASM: Rust’s ownership model is quite compatible with WASM.
3. Java and C# (and JavaScript as well) need a garbage collector and threading.

But WASM doesn’t use a garbage collector, so a common approach is to take a garbage collector and compile it to WASM. You can find C++ garbage collector implementations, and you can compile and ship that as part of your application. That’s going to add extra size, bloat and is pretty inefficient. So At some point in the future, WASM will likely support garbage collection. Maybe: rather than having its own garbage collector, it will interact with the host’s garbage collector.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

And at the moment WASM's threading model is the same as JavaScript's: a single thread of execution. When you invoke a WASM function, your JavaScript virtual machine yields to WASM. So you won’t have JavaScript and WASM running in parallel. You can have web workers, just like you can in JavaScript, so you can parallelise like that.

# WASM use cases

- heavily CPU-bound number computations e.g. games (via opengl)
- you'll be consuming compiled binaries

## What success stories are there of people using WASM?

Not too many at the moment - because it’s quite a new technology
Some of the interesting examples are coming from Mozilla, because they’re a big backer of WASM.

The interesting examples are where the complexities of JavaScript and WASM interfacing is minimised, because they’re doing very simple things. You won’t find people using WASM to work in React, or DOM manipulating applications.

16:25 A really interesting one that Mozilla published is part of our common toolchain was to assist with sourcemaps, a JS technology to map minified or transpiled code back to the original source.
16:40 It’s very widely used and very important for a lot of people.
16:45 Mozilla took the JavaScript used to generate sourcemaps, and ported it to web assembly and runs approximately three times faster.
16:55 From reading the blog post [https://hacks.mozilla.org/2018/01/oxidizing-source-maps-with-rust-and-webassembly/], it sounds like it will be released to production soon.
17:00 At the moment it’s being used for fairly specialised algorithmic tasks.
17:05 Web assembly is at the minimum viable product (MVP) stage and a young technology.
17:10 The feature set is deliberately minimal - as the feature set expands along with the toolchain and the ecosystem - we’ll start seeing it used for all sorts of things.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

# WASM history and ecosystem

## History and ecosystem

WASM is an MVP
2015: WASM community group
2017: cross browser consensus
2018: draft of the specification 1.0: WASM core spec (=syntax, naming, building, validayion, execution + the standard for the binary format ie types and values), WASM JS interface (interactions between WASM modules and JS, data storage, sandboxing), WASM web API (rules about module compilation and interactions between the dom and the WASM modules)

ASM paved the way to WASM.

## the WASM organism

# WASM in the browser

## Prerequisite: main building blocks of a browser

what happens at runtime? what gets loaded onto the browser, what gets executed, and by what????

When a browser receives JS code, it needs to execute it.
But JS is a high-level language, that the computer doesn't understand as is.

Need for a JS ENGINE (also referred to as a COMPILER): a program that takes human-readable source code (in our case JavaScript), and from it generates machine-readable instructions (= MACHINE code = NATIVE code) for your computer.
"Compiling" in the browser context implicitely means "compiling to MACHINE CODE".

In the past:
Before V8 and other compilers, Javascript was interpreted (= dealt with by interpreter). That was slow.

Now:
From 2012 on, browsers have been implementing new Javascript engines, trying to COMPILE some portions of code, to speed Javascript up. Most browsers today do high-perf, optimized JIT (just-in-time) compiling.

For example, V8 is Google’s open source high-perf JavaScript and WebAssembly engine. It's written in C++ and implements ECMAScript and WebAssembly. V8 can run standalone or embedded into any C++ application ; it's used in Google Chrome, Node.js and others.

Sources:
https://v8.dev/
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file

### Disambiguation: engine vs VM

An engine, like V8, is a type of VM.
A runtime is a VM ; i.e. everything needed for the code to run.

- What happens when I run C code on my computer? And rust code? and JS code? what's compiled, what's not, what uses a vm?

### What an engine does

Actually, an engine is more than just a compiler.

With JS code:

-

With webassembly code:

## flow: How does wasm inject itself into a web page

Imagine we're creating a WASM module that just adds a couple of numbers together:

Build
write it in a high level language (rust or C++)
take a toolchain for that language to compile it into a wasm binary.
Run

- Because The wasm binary itself has sections within it that export and import functions (similar to JavaScript modules, which export and import functions): the JS code will load up the wasm code, and you’ll be able to see it and invoke it from JavaScript.
- Under the hood, rather than that function being interpreted as JavaScript code, that function will be the web assembly virtual machine.

That’s how you currently load wasm modules through JavaScript to invoke compiled code.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Browser support

Since late 2017, WASM is supported in all modern major browsers (Chrome, Firefox, Safari and Edge)

---

# Challenges & future of WASM

## Challenges today

WASM only has four types at the moment; they’re all numeric (two integer types and two floating point types).
So: implementing a WASM function that adds two numbers is fairly trivial; but Strings are more difficult.
One way to handle string data at the moment is to use linear memory; it has memory that you can read and write to from WASM and JavaScript.
The interesting thing here is to model strings, you share the same piece of memory with null-terminated data.
Real hello world application would look a bit complicated and slightly strange, which is why people who use it use a high-level toolchain
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

Challenge at the moment: there’s quite a lot of complexity involved in interfacing between JavaScript and web assembly. Calling functions is really easy - you can send stuff backwards and forwards, but it’s the types that you’re sending back and forth that is the challenge.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Future

Currently: WebAssembly 1.0 has shipped in 4 major browser engines.

WASM 2.0: multi-threading model and garbage collection (C# and Java), multi-value returns, host binding (it will be easier to expose JavaScript objects to WASM), Integrating WASM modules with JavaScript modules.

webpack support would be awesome: rust-loader, cpp-loader

Q: where at is the direct access to web apis? (wasm only)

WASM has the power of

- Breaking down the monopoly. The web is the most ubiquitous platform that we have at the moment, and it’s quite bad that we only have one language that has first class support. The web will open up to many other developers like C#, Java... !
- Existing web developers, who are comfortable with JavaScript or TypeScript, will start looking at the performance benefits of WASM, and they’ll want to be part of it too.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

# Disambiguations

## WASM vs WebGL?

They are rather unrelated, but can be used together.

WebGL is a browser's API onto the machine's GPU (= graphical processing unit = 3D hardware). It's based on the OpenGL standard.

Web developers can use JS/WASM/... to access WebGL when they need to do 3D graphics fast.

More: https://getpocket.com/a/read/2365657803

## GPU, CPU, WASM

## WASM vs ASM

ASM is a mozilla-built PoC of a low-level virtual machine out of JavaScript. They took a very strict subset of the language, and like WASM they have the concept of memory being an array. They defined their own language, on top of JavaScript. They built into their own browser something that understood the language they’d created, and optimised for it. The whole thing was a very clever and slightly crazy experiment, but it worked.

ASM and WASM are similar - they define an assembly-like set of instructions.
Problems of ASM.js:

- it is coded in JavaScript so is quite verbose and difficult to understand syntax.
- In addition, it is only optimised for Firefox (?).
  In hind-sight, it looks like a very early proof of concept for WASM.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## How is WASM different from writing, say, Flash?

3:35 Part of the reason why people think it sounds similar is because one of the motivations of creating WASM is to create a new assembly language which is a compilation target for a range of high level languages.
3:50 So C#, Java, Rust, C++ and others are now able to be compiled into WASM and run in the browser.
4:00 That immediately makes people think of how they used to be able to run those kind of languages in the browser.
4:05 There are some very fundamental differences in the way this is being achieved.
4:15 Flash, Silverlight and so on used the plugin model, which is a bolt-on to the side of the browser that lets you have a different execution environment and a restrictive API to communicate between that runtime and the first-class runtime in the browser.
4:30 Web assembly isn’t like that; it is very tightly integrated within the JavaScript virtual machine, and there’s a very close synergy between the two.
4:45 The other difference is in the way it was created.
4:50 Silverlight was an invention pushed by Microsoft; Flash was an Adobe creation [ed: FutureWave created Flash, who were then acquired by Macromedia and then subsequently Adobe].
5:00 They were created in an era of competition, and they were different plugin vendors and browsers.
5:10 Web assembly was created through collaboration, with significant representation from browser vendors.
5:20 That has a significant impact on its adoption; it’s been adopted and moved into production browsers in a very short space of time.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## is WASM a JS killer?

Early stage adopters of WASM are going to use it because of the speed advantages it offers, and its ability to port existing programs to the web, rather than as a rejection of JavaScript. As we move on, however, it should be possible to write in whatever language you like, compile it to WASM, and run it in any browser. This is seen by many as a future world in which JavaScript no longer rules the web. Is this likely? There is a great deal of investment in JavaScript and WASM is designed to run on the same engine that runs it, so it isn't going to be disadvantaged by the adoption of WASM. At the moment WASM still needs JavaScript to do things like interact with DOM and this makes it a partnership. If a JavaScriptless future is going to be a reality then WASM has to be expanded a lot, and this might not happen if interworking with JavaScript is a cheaper option. It really might turn out to be a partnership rather than a takeover.
https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

# FAQ

## Is WASM ready for production use?

It’s called assembly - if you look at the way that PIC micro-controllers and 6502 processors, it’s very similar - none of them understand strings.
It doesn’t mean that you can’t write applications just because the processor doesn’t have an innate understanding of what a String is.
It just means that most people won’t write the assembly language directly; they’ll rely on a compiler where someone else has done all the magic.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Doesn’t the advent of WASM mean that we will see larger binaries being delivered to clients?

Good question - because if a desktop executable is 50Mb or 100Mb it generally doesn’t matter - but if you add an extra 20% payload to a website, people care about that.

Should be OK, because:

- Technically speaking, if you take a single algorithm and you compile that to minified JavaScript and separately compile it to WASM, the WASM will be smaller because it’s a binary format.
- Within the web we’ve optimised for performance and size (whereas on the desktop there hasn’t been that much pressure) On the web, we have the notion of bloat, and adapted tooling: with Bootstrap, you can customise your own build, for JavaScript you can use tree shaping, which means you only deliver the required code to the browser... etc.
- You can create bloat in any technology anyways - you’ll find people putting JQuery in the page to use a single function, or all of Bootstrap when they’re only using one or two classes.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## What will happen to web frameworks?

WASMi s an efficient runtime, but it doesn’t have direct access to the DOM API and maybe never will.

Also: although it’s got the name web in it, they have been quite careful to ensure that it will work well in other execution environments.

The future of a web application might be 70-80% WASM, and the rest being JavaScript - the glue that marshals access to the DOM and CSS across its host bindings. For a native mobile application, you might have the same 70-80% WASM, but a different host binding system for the mobile device.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## What will web look like five years from now?

- we’ll still be using the browser, because it’s a fantastic distribution mechanism. Think of how email changed!! The web and browsers aren’t going away.
- But: JavaScript might lose its monopoly, and I do see people writing significant applications using a wide variety of languages on the web.
- there’s a chance that WASM will have an impact far beyond the web itself.
- We also know that on the desktop, the number of applications that are being written specifically for the desktop are diminishing over time. Add WASM to the mix, and you can start distributing applications that do heavy lifting, like CAD applications or PhotoShop.
- a certain class of application that we still struggle to distribute as a web application today will be possible.
- see it not only having an impact on the web, but also on desktop and mobile as well.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

# Tools & Resources

## Tools

https://mbebenita.github.io/WasmExplorer/
https://webassembly.studio/

## Curated list

https://github.com/mbasso/awesome-WASM

## Benchmarks

https://pspdfkit.com/blog/2018/a-real-world-webassembly-benchmark/
https://medium.com/@torch2424/webassembly-is-fast-a-real-world-benchmark-of-webassembly-vs-es6-d85a23f8e193
https://lemire.me/blog/2018/10/23/is-webassembly-faster-than-javascript/

# Appendix

## Where did JavaScript come from leading to today?

Prior to JS, the web was a very static place: If you wanted to create interactivity in the browser, it involved a round-trip to the server.

JS was designed to support a modest amount of interactivity client-side, such as form validation.

So JS was developed in a short space of time, and everyone knows it’s a bit of a quirky language. Browser makers spend a lot of time testing to make sure changes don’t break existing websites.

No one expected it to become as fundamental as it has become.

JS has become a runaway success - not just within the browser, but extensively on the mobile or smart watches. You can run JavaScript programs anywhere.
JS is now very mature - it’s evolving at a rapid space. When new language features come along, transpilers can be used to backport those features into older versions of JavaScript.

## A short browser history

- 1995: /index.html = static HTML content
- 2005: /index.php = dynamic content generated from server-side code
- TODAY: /api/v1/todos = semi-raw data in a browser-understandable format

So far JS was the only language that could be run by browsers ; it was mostly designed for user interactions, but now we can build fully-fledged apps with it
--> How to make it faster?

- use a framework
- precompile: TypeScript, Dart

Wait. Can a webpage run at hardware-native speed?
Yes, With WASM.

source: https://fosdem.org/2019/schedule/event/the_state_of_webassembly_in_2019/

## About the WASM logo

A cute feature of the logo is that the notch in the top enables it to connect with the JavaScript logo.

# Inbox

### ASM, AST
