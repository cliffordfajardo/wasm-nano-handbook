# Wasm: Vision // 🚧WIP

_On what WebAssembly is, and where it is taking us to._  
_↠ Up Next: [Language](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-language.md)._

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/vision.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

## ⚡ TL;DR

Wasm not here to replace JS. JS and Wasm will help each other (and us) make the web better.
Wasm is still at an early stage, but it's already available in all major browsers.

## So, what is Wasm?

**WebAssembly is a new efficient, low-level assembly-like language that runs at near-native speed in all modern browsers ; it's debuggable and part of the open web. Wasm can also be used as a compilation target for a wide range of other languages ; it is designed around portability and safety.**

OK. That was a mouthful.

Let's decrypt this, one piece after another.

> New

Wasm 1.0 is an MVP. As mentioned before, the idea behind wasm is not new, though. Wasm is the combined solution of different attempts to solve the same problem.  
One thing to keep in mind is that because it's new, it's moving - and rather fast.  
MDN has fantastic documentation for basic to intermediate cases ; but if you're in the mood to try more experimental things, you'll need to do some reading on how things work.

> Efficient

This implicitely means _in comparison to JS_. Even minified JS is text, whereas Wasm is a binary format. A binary format is more compact. It takes up less bandwidth (fast travel over the network) and less storage space.

> Low-level assembly-like

This simply means that WebAssembly is closer to machine code than a language like JS. That is what makes it fast.  
Because it's close to machine code, you typically wouldn't write it by hand. We'll dive deeper into the language in the Language chapter.

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

Portability means that Wasm can be run on mutliple browsers, platforms, environments and devices.

- First, any environment that embeds a JS engine - understand, a browser or node - can already run Wasm code.
- So Wasm can be run on the web, but it doesn't _need_ a JS VM to run. It has an import/export mechanism that's environment-agnostic. You could import C functions into a wasm module, and export wasm functions back to use them in your C application. Also, the Wasm spec is clear on that point: even if Wasm was primarily built with the web in mind, a wasm module won't _require_ web APIs to run.
- Wasm's spec is rather small and simple compared to ther formats. This means that implementing support for it is simple.
- Wasm takes advantage of common hardware capabilities available on a wide range of platforms, including mobile and IoT. Understand: wasm doesn't require a crazy 20-core achitecture ; all it needs to run is what the simplest Rasperry Pi can offer.

https://webassembly.org/docs/non-web/
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

There are even cross-platform Wasm virtual machine projects, such as Life and wasmer.
You could run wasm in your frontend, your backend, a servers in datacenters, IoT devices, a desktop apps, or even embedded within larger programs. Using Wasm like this, as a portable binary format on many platforms would bring great benefits in portability, tooling and language-agnosticity.

## Use cases

- web: heavily CPU-bound number computations e.g. games (via opengl)
- web: Deliver existing C/C++/... applications over the web (Talking about things like games, 3D Graphics and more)
- web: Accelerate hot code portions of ordinary JavaScript apps
- web/others: you'll be consuming compiled binaries
- web/others: Develop in your language of choice (for example .NET or Java).


## Future
Link to specs
