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

Wasm is the result of a concerted approach to improve web performance and build more flexibily for the web. Its features also make it fantastic for use cases outisde the web. It's not here to replace JS - the same way X and Y coexists, JS ans Wasm will help each other (and us) to make the web better.
Wasm is still at an early stage, but it's already available in all major browsers.  
Think of it like the `fetch` API or `localStorage`: it will soon become part of your toolbox.

## Reasons to care

Wasm is not a new framework. It's a whole new universe

<!-- which you could hesitate to learn because it's just hype.
It's an actual new tool that's embedded in browsers.
It's as serious as the new ES6 syntax was, or as any cross-browser feature. -->

## Origins

### Hard times of Old Web Land

OK, that's overdramatic - The web is great, and JS is great!

But they're not perfect.

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

Let's take a closer look at how (1) and (2) impact both the developer experience and the user experience.  
As it turns out, (1) tends to impact DevX while (2) tends to impact UX.

- Web apps can get slow.
- Some use cases are simply not supported on the web. This is an extension of the previous point: infinitely slow is just not an option.
- Our CPUs are under stress. Because JS used to run very slowly, browser engines teams have designed advanced optimization techniques to make it run faster, such as JIT (Just-in-Time compiling ; TBD link. Don't worry if you don't know what this is, we'll cover that later). This proved very effective: JS today runs manyfold faster that it used too - it was a huge leap. But nothing comes for free. Running JS fast is resource-intensive, especially on smaller devices such as smartphones.
- The power of millions (yes, millions) of native developers is not leveraged for the web. Inversely JS devs as of today can't build for truly native performance.
- No flexibility when writing for the web
- The JS toolchain is convoluted. There are a ton of tools out there that help us developers deliver JS code that loads and runs as fast as it gets. That is both amazing and overwhelming - it gets difficult to keep up.

### Solution

(1) and (2) are not new problems. Different actors and organizations have attempted to solve them in the past. All these approaches were innovative and solved some part of the problem, but none of them really won the game.  
You think things have always been like today.

Let's have a quick look at them to better understand what makes Wasm special:

- PNcl:
- browser plugins:
- p language:
- asm.js

Their success was always mitigated: the performance was better, but not consistently better ; or the approach worked but not on all browsers ; or not cross-platforms e.g. not on mobile devices. (TBD link and details: Alex Danilo on browser plugins, ASM.js, PNaCl, p-code ; google i/o 17 https://www.youtube.com/watch?v=6v4E6oksar0)

Luckily, all these approaches have brought us forward: the people and organizations working on them built up a solid experience.

### Re:Solution

Later on, they joined forces to think of a sustainable, cross-browsers, cross-platforms solution to (1) and (2): **WebAssembly, or Wasm for short**.

**So, Wasm is born for the web.**

But in fact, there is way more to it - because it's also a compilation target, **its benefits go way beyond the web**.

## So, what is Wasm?

**Wasm is a new efficient, low-level assembly-like language / bytecode,** that:  
(3) runs at at near-native speed [performant](4) on all modern browsers [portable](5) and is a compilation target for a wide range of other languages such as C++ and Rust [portable].

Wait, how new?
Wasm 1.0 is an MVP, that has shipped in 4 major browser engines.

- (5): there is consensu around it. Understand: that is also part of what makes it special.
  Other core features:

- (6) safe
- (7) debuggable
- (8) part of the open web.

Let's walk through these characteristics, to understand what makes Wasm powerful:

(3) Efficiency

- has bindings that enable that code to access the capabilities of the browser / of JS

(4) and (5) Portability

- One of the strengths of Wasm is the **consensus** there is around it.
- But it's also technically designed for portability.

Wasm could be used as a portable binary format on many platforms, bringing great benefits in portability, tooling and language-agnosticity.

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

> “Open web” is a sweeping term — it encompasses technical concepts like open-source code and open standards. But there’s a single underlying principle connecting all these ideas: An open web is a web by and for all its users, not select gatekeepers or governments. (...) we compare the open web to a global public resource, like clean water or the environment.  
> https://www.yearofopen.org/november-open-perspective-what-is-open-web/what-is-the-open-web-and-why-is-it-important-submitted-by-mark-surman-executive-director-of-the-mozilla-foundation/

Sources:  
https://webassembly.org/

## Game changer

Now it's not an overstatement to say that Wasm will change .
It will change what we build, how we build it, but also who builds it.

Why it will change the world? / Benefits 🚧WIP

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
