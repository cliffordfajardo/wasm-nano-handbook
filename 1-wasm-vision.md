# Origins and Vision // 🚧WIP

_On what WebAssembly is, where it comes from, and where it is taking us to._  
_Up Next: [Language](https://github.com/maudnals/wasm-nano-handbook/blob/master/2-wasm-language.md)._

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/vision.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>   
 
[1. Origins](https://github.com/maudnals/wasm-nano-handbook/blob/master/1-wasm-vision.md#origins)     
[2. So, what is Wasm?](https://github.com/maudnals/wasm-nano-handbook/blob/master/1-wasm-vision.md#so-what-is-wasm)      
[3. Game-changer](https://github.com/maudnals/wasm-nano-handbook/blob/master/1-wasm-vision.md#game-changer)  
[4. Use cases](https://github.com/maudnals/wasm-nano-handbook/blob/master/1-wasm-vision.md#use-cases)      
[5. Time travel](https://github.com/maudnals/wasm-nano-handbook/blob/master/1-wasm-vision.md#time-travel)

## ⚡ TL;DR

Wasm is the result of a concerted approach to improve web performance and build more flexibily for the web. Its features also make it fantastic for use cases outside the web. It's not here to replace JS - the same way X and Y coexists, JS ans Wasm will help each other (and us) to make the web better.
Wasm is still at an early stage, but it's already available in all major browsers.  
Think of it like the `Fetch` API or `localStorage`: it will soon become part of your toolbox.

## Reasons to care

Wasm is not a new framework. It's a whole new universe

## Origins

### Hard times of Old Web Land

OK, that's overdramatic - The web is great, and JS is great!

But we can take them to the next level.

When building and running web apps, we must face two significant constraints:

- (1) Browsers, one of the most ubiquitous pieces of software, can only be targeted with **one single language**: JavaScript. Or so was it, until recently.
- (2) JS loads and runs **slower** than native code.

When you look at the web today, these might not seem like huge issues. Web apps are running, the world is using them, JS is evolving, and JS developers won't go extinct.

Right?

Right. But it's not just about today ; it's also about the **delta** between now and the future.  
Compare what the web is now with _what the web could become_.  
It suddenly makes a lot of sense to break free from these constraints.

<p align="center">
<img width="720" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/delta-2.jpg">   
 <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

### Build time pain, runtime struggle

Let's take a closer look at how (1) and (2) impact both the developer experience and the user experience.  
As it turns out, (1) tends to impact DevX while (2) tends to impact UX.

- Web apps can get slow.
- Some use cases are simply not supported on the web. This is an extension of the previous point: infinitely slow is just not an option.
- Our CPUs are under stress. Because JS used to run slowly, browser engines teams have designed advanced optimization techniques to make it run faster. JIT (Just-in-Time compiling) is one such example. Don't worry if you don't know what this is, we'll cover that later. JIT proved very effective: JS today runs manyfold faster that it used too - it was a huge leap. But nothing comes for free. Running JS fast is resource-intensive, especially on smaller devices such as smartphones.
- The power of millions (yes, millions) of native developers is not leveraged for the web. Inversely JS devs as of today can't build for truly native performance.
- We lack flexibility when writing for the web: JS is our only choice.
- The JS toolchain is convoluted. There are numerous of tools out there that help us developers deliver JS code that loads and runs as fast as it gets. That is both amazing and overwhelming - it gets difficult to keep up.

### Solution

(1) and (2) are not new problems.  
Different actors have attempted to solve them in the past, by running native(-ish) code in the browser:

- Browser plugins, such as Flash: Plugins were great in their time. But: they created security issues, couldn't leverage Web APIs, and didn't play out great on mobile.
- Portable Native Client: PNaCl was developed by Google, and could run code fast. But its architecture was rather complex and it only ran on Chrome.
- asm.js: Backed my Mozilla, asm was a subset of JS that could be run really fast by Firefox - but not consistently fast. Also, asm was _still_ JS, i.e. a rather inefficient text format. And just like PNaCl, it didn't propagate to other browsers.

(TBD link and details: Alex Danilo on browser plugins, ASM.js, PNaCl, p-code ; google i/o 17 https://www.youtube.com/watch?v=6v4E6oksar0)

All these approaches solved some aspect of the problem. But none of them really won.  
Luckily, they have brought us forward: the people and organizations working on them built up experience.

### Re:Solution

Later on, they joined forces to think of a safe cross-browsers solution to (1) and (2), that wouldn't suffer from the pitfalls of the previous solutions.

**WebAssembly** was born.

**So, Wasm was created with the web in mind.**

But in fact, there is way more to it - because it's also a compilation target, **its benefits go way beyond the web**.

## So, what is Wasm?

**WebAssembly is a new efficient, low-level assembly-like language that runs at near-native speed in all modern browsers ; it's debuggable and part of the open web. Wasm can also be used as a compilation target for a wide range of other languages ; it is designed around portability and safety.**

OK. That was a mouthful.

Let's decrypt this, one piece after another.

> New

Wasm 1.0 is an MVP, that has shipped in 4 major browser engines in 2018. As mentioned before, the idea behind wasm is not new, though. Wasm is the combined solution of different attempts to solve the same problem.

> Efficient

This implicitely means _in comparison to JS_. Even minified JS is text, whereas Wasm is a binary format. A binary format is more compact. It takes up less bandwidth (fast travel over the network) and less storage space.

> Low-level assembly-like

This simply means that WebAssembly is closer to machine code than a language like JS. That is what makes it fast.  
Because it's close tp machine code, you typically wouldn't write it by hand. We'll dive deeper into the language in the Language chapter.

> Runs at near-native speed

Benchmarks have showed that Wasm runs at 1.2x native speed.

> In all 4 major browsers

Chrome, Firefox, Safari and Edge have built-in Wasm support. There is more to this info than it looks. Not only does this mean that you can ship wasm to all these browsers ; it also means that there is _consensus_ around WebAssembly. Wasm is a standard.

> Part of the open web

> “Open web” is a sweeping term — it encompasses technical concepts like open-source code and open standards. But there’s a single underlying principle connecting all these ideas: An open web is a web by and for all its users, not select gatekeepers or governments. (...) we compare the open web to a global public resource, like clean water or the environment.  
> https://www.yearofopen.org/november-open-perspective-what-is-open-web/what-is-the-open-web-and-why-is-it-important-submitted-by-mark-surman-executive-director-of-the-mozilla-foundation/

Actors from multiple organizations have a say in how Wasm will develop.

> Can be used as a compilation target

Wasm's design makes it easy for many other languages to be compiled _into it_.  
This widens the entry surface for Wasm code - think of it like English. Many humans speak English - that makes it easier to talk to each other. Some think of Wasm as the way to universal libraries!  
C++ and Rust offer the best support for wasm today, but there are alternatives. We'll touch on that later.

> designed around safety...

Safety is a big deal on the web. Browsing is essentially allowing your computer to download untrusted code from anywhere in the world, and execute it.  
The reason your computer and the world haven't burst into radioactive flames yet is called sandboxing. Sandboxing means that your code is run is a close, safe environment. A Wasm application runs inside a sandbox.
Wasm's security model also protects developers from control flow hijacking, and various memory errors. This is important because languages with a managed memory (understand: manually managed - this is the case of C++ and Wasm) are usually prone to developer errors.

> ... and portability

(4) and (5) Portability

Wasm could be used as a portable binary format on many platforms, bringing great benefits in portability, tooling and language-agnosticity.

has bindings that enable that code to access the capabilities of the browser / of JS

https://webassembly.org/docs/non-web/

(4) and (5)
Because:

- it runs on the web (JS VM supports Wasm), which is on a lot of platforms
- Non-Web environments may include JavaScript VMs (e.g. node.js), however WebAssembly is also being designed to be capable of being executed without a JavaScript VM present.
- it takes advantage of common hardware capabilities available on a wide range of platforms, including mobile and IoT.
- the plan is to keep non-Web path such that it doesn’t require Web APIs (the core features will be within Wasm itself: certain features that are core to Wasm semantics that are similar to functions found in native libc would be part of the core Wasm spec as primitive operators)
- because it's closer to machine language (it supports C/C++ level semantics), VMs are easier to implement on multiple platforms
- There is even a project for a cross-platform Wasm virtual machine: Life is written in Go, built for running computationally heavy code on practically any device you can imagine.
- its AMI is platform-agnostic:
  WebAssembly does not specify any APIs or syscalls, only an import mechanism where the set of available imports is defined by the host environment. In a Web environment, functionality is accessed through the Web APIs defined by the Web Platform. Non-Web environments can choose to implement standard Web APIs, standard non-Web APIs (e.g. POSIX), or invent their own.

e.g. on servers in datacenters, on IoT devices, or mobile/desktop apps, or even embedded within larger programs.

Sources:  
https://webassembly.org/

## Game changer

Wasm will change what we build, how we build it, and also who builds it.

Why that?

1. UX: Wasm will make (the web) faster  
   Native speed  
   also see WebAssembly Parallelism / Threads

2. Wasm will accelerate the future of web development

- New performance-demanding use cases become accessible to the web
- New libraries become accessible to the web
- Wasm breaks down the JS monopoly...
  Wasm enables linguistic diversity ; this will dramatically diversify the languages available for building front-end applications and tools. Web development will become accessible to developers coming from other languages ; JS developers will benefit from their experience, and inversely.
- ... and helps JS win  
  Wasm will grow to include lots and lots of expressiveness for lots and lots of languages, JS included.
  With shared array buffer extension, eventually all the browsers and webviews will support Wasm syntax to serve the compile target master, and free JS so it can serve the JS master.
- Wasm can be used as a laboratory for the future of the web  
  https://zendev.com/2018/06/26/webassembly-accelerating-future-web-development.html

3. DevX: Wasm could make our lives easier
   Not just on the web! Languages interop is complicated, and Wasm can help.  
   Developer experience: no more tower of Babel

4. More

## Use cases

- web: heavily CPU-bound number computations e.g. games (via opengl)
- web: Deliver existing C/C++/... applications over the web (Talking about things like games, 3D Graphics and more)
- web: Accelerate hot code portions of ordinary JavaScript apps
- web/others: you'll be consuming compiled binaries
- web/others: Develop in your language of choice (for example .NET or Java).
