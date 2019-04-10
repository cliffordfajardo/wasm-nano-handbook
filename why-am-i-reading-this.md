# Why am I reading this?

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/why-am-i.jpg">  
  <div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

Good question.

Why would developers want to learn about WebAssembly over spending time on other techs/tools?

Picture yourself, on a weekday morning. You're drinking the Hot Drink while opening your tech newsletters.
A new tool/framework is making headlines.  
**What do you do?**

1. Laugh and burn these pixels
2. Keep that tool/framework in mind. You'll come back to it later when/if it has taken off.
3. It catches your attention. You give it a try, you love it, you adopt it. Until the next best tool comes in, in which case you might go for option 1.

WebAssembly is to this tool/framework what the moon is to a street lamp.  
**They look the same from afar, but really they're not**.

### Wasm is not just a new hype thing. It is both highly transformative and here to stay.

How is that?

## 1. A matter of space

WebAssembly (Wasm for short) is a flexible technology that doesn't make assumptions about where it runs. You could use it in a wide variety of environments.

Luckily, some environments have already taken care of integrating it.  
And these environments are ubiquitous: Wasm is supported in **all four major browsers** (Chrome, Edge, Firefox, and WebKit/Safari). This means it's **already usable almost everywhere**.

Besides, it's part of the web platform. Browser APIs for WebAssembly are like the Fetch API or the Web Workers API. They're standards. Standards are solid.

Last but not least: the WebAssembly Community Group is backed by w3c and its members represent four browsers. You'd have guessed that Wasm is not going extinct anytime soon - quite the contrary, this is just the start.

## 2. There's _early_ and _early_

When learning about Wasm, you might often read/hear the words _MVP_ and _early_. It is indeed a young technology.  
However:

- Being young doesn't make it non-production-ready. It is.
- This isn't greenfield. Wasm is the **joint result** of approaches from Chrome teams, Mozilla teams, and many others. It builds upon their accumulated knowledge when trying to solve the same issues. Wasm is the solution for which the consensus is the strongest.

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/sketchup.png">  
  <div align="center"><sub><sup>SketchUp in production, using wasm modules</sup></sub></div> 
</p>

## 3. No borders aka _It's not just fast_

Speed in the browser is certainly one benefit of Wasm. It makes performance-demanding web apps possible.

**But it's only one part of the story.**  
Since Wasm is also a compilation target, it can transform:

- How we write apps // e.g. write in C++ for the web
- Where code runs // e.g. a wasm module could run anywhere -> a way to universal libraries?

What this means: Wasm may **diffuse through mutiple layers of your stack**, web or non-web.

## 4. Under the hood

Understanding Wasm goes hand-in-hand with understanding how JavaScript (JS) runs. Not just the event loop and the callback queue, but how browsers actually execute JS code.  
After all, this is at the core of how web apps work. Kind of good to know!

**To be clear:** you don't _need_ to understand browser internals to use it ; it's just something you get for free if you understand Wasm.

<p align="center">
<img width="380" src="https://cdn-images-1.medium.com/max/1440/1*ZIH_wjqDfZn6NRKsDi9mvA.png">  
  <div align="center"><sub><sup>Chrome V8’s compiler pipeline by @fhinkel - https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775</sup></sub></div> 
</p>

## Good news

Wasm's basics are simple, and it's a breeze to try it out.

So, let's go!  
↠ Up next: [Wasm: Origins](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-origins.md).
