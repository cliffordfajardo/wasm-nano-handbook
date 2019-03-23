# Why am I reading this? 


<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/why-am-i.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>   



Good question.

Why would developers want to learn about WebAssembly over spending time on other techs/tools?

Picture yourself, on a weekday morning, drinking the Hot Drink while opening your tech newsletters.
A new tool/framework is making headlines.  
**What do you do?**

1. Laugh and burn these pixels
2. Keep that tool/framework in mind, and come back to it later when it has taken off.
3. It catches your attention, you give it a try, you love it, you adopt it. Until the next best tool comes in, in which case you might go for option 1.

WebAssembly is to this tool/framework what the moon is to a street lamp - **they look the same from afar, but really they're not**.

### Wasm is not just a new hype thing. It is both highly transformative and here to stay.

How is that?

## 1. A matter of space

WebAssembly (Wasm for short) is a flexible technology that doesn't make assumptions about where it's being run ; you could use it in a wide variety of environments.

Luckily, some environments have already taken care of integrating it.  
And these environments are ubiquitous ones: Wasm is supported in **all four major browsers** (Chrome, Edge, Firefox, and WebKit). This means it's **already usable almost everywhere**.

Besides, it's part of the web platform. Browser APIs for WebAssembly are similar to the `fetch` API. It's a web standard. Standards are solid.

And because the WebAssembly Community Group members represent four browsers and is backed by w3c, Wasm's future tends to be bright and safe.

## 2. There's "early" and "early"

When learning about Wasm, you might often read/hear the words "MVP" and "early". It is indeed a young technology.  
However:

- Being young doesn't make it non-production-ready. It is.
- This isn't just greenfield ; Wasm is the **joined** result of various approaches. It builds upon previously accumulated knowledge, and there is a strong consensus around it.

## 3. No borders aka "It's not just fast"

Speed in the browser is certainly one benefit of Wasm. It makes performance-demanding web apps possible.

**But it's only one part of the story.**  
Since Wasm is also a compilation target, it can transform:

- How we write apps // e.g. write in C++ for the web
- Where code runs // e.g. a wasm module could run anywhere -> a way to universal libraries?

What this means: Wasm may **diffuse through mutiple layers of your stack**, web or non-web.

## 4. Under the hood

Understanding Wasm goes hand-in-hand with understanding how JavaScript (JS) runs - not just the event loop and the callback queue, but how browsers actually execute JS code.  
After all, this is at the core of how web apps work. Kind of good to know!

**To be clear:** you don't _need_ to understand browser internals to use it ; it's just something you get for free if you understand Wasm.

## Good news

Wasm's basics are simple, and it's a breeze to try it out.
