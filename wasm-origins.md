# Wasm: Origins

_On what WebAssembly is, where it comes from, and where it is taking us to._  
_Up Next: [Vision](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-vision.md)._

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/vision.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

## ⚡ TL;DR

Wasm is the result of a concerted approach to improve web performance and enable more flexibility for the web - and outside of it.

## Hard times of Old Web Land

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

## Build time pain, runtime struggle

Let's take a closer look at how (1) and (2) impact both the developer experience and the user experience.  
As it turns out, (1) tends to impact DevX while (2) tends to impact UX.

- **Runtime/UX impacts**:
  - Web apps can get slow.
  - Some use cases are simply not supported on the web. This is an extension of the previous point: infinitely slow is just not an option.
  - Our CPUs are under stress. Because JS used to run slowly, browser engines teams have designed advanced optimization techniques to make it run faster. JIT (Just-in-Time compiling) is one such example. Don't worry if you don't know what this is, we'll cover that later. JIT proved very effective: JS today runs manyfold faster that it used too - it was a huge leap. But nothing comes for free. Running JS fast is resource-intensive, especially on smaller devices such as smartphones.
- **Build time/DevX impacts**:
  - The power of millions (yes, millions) of native developers is not leveraged for the web. Inversely JS devs as of today can't build for truly native performance.
  - We lack flexibility when writing for the web: JS is our only choice.
  - The JS toolchain is convoluted. There are numerous of tools out there that help us developers deliver JS code that loads and runs as fast as it gets. That is both amazing and overwhelming - it gets difficult to keep up.

## Solution

(1) and (2) are not new problems.  
Different actors have attempted to solve them in the past, by running native(-ish) code in the browser:

- Browser plugins, such as Flash: Plugins were great in their time. But: they created security issues, couldn't leverage Web APIs, and didn't play out great on mobile.
- Portable Native Client: PNaCl was developed by Google, and could run code fast. But its architecture was rather complex and it only ran on Chrome.
- asm.js: Backed my Mozilla, asm was a subset of JS that could be run really fast by Firefox - but not consistently fast. Also, asm was _still_ JS, i.e. a rather inefficient text format. And just like PNaCl, it didn't propagate to other browsers.

(TBD link and details: Alex Danilo on browser plugins, ASM.js, PNaCl, p-code ; google i/o 17 https://www.youtube.com/watch?v=6v4E6oksar0)

All these approaches solved some aspect of the problem. But none of them really won.  
Luckily, they have brought us forward: the people and organizations working on them built up experience.

## Re:Solution

Later on, they joined forces to think of a safe cross-browsers solution to (1) and (2), that wouldn't suffer from the pitfalls of the previous solutions.

**WebAssembly** was born.

**So, Wasm was created with the web in mind.**

But in fact, there is way more to it - because it's also a compilation target, **its benefits go way beyond the web**.

Really? Let's explore what makes Wasm powerful.
Up next: [Wasm: Vision](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-vision.md).
