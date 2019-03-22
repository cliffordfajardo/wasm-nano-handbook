# Why am I reading this

Good question, why?

Why would developers want to learn about WebAssembly (Wasm for short)?  
Why spend the next minutes reading about Wasm _over_ other techs/tools?

Picture yourself, on a weekday morning, opening your tech newsletters.
A new tool/framework is making the headlines.  
What do you do?

1. Laugh and burn these pixels
2. Keep that tool/framework in mind, and come back to it later when it has taken off. Early tech = Uncertain survival.
3. It catches your attention, you give it a try, you love it, you adopt it. Until the next best tool comes in, in which case you might go for option 1.

WebAssembly is to this tool/framework what the moon is to a street lamp - they look the same from afar, but really they're not.

**Wasm is not just a new hype thing.**
It is both **highly transformative** and **here to stay**.

How is that?

## 1. A matter of space

Wasm is supported in **all 4 major browsers**; this means that the possibility of Wasm is already almost everywhere.

Wasm is part of the **web platform**. Wasm browser APIs can be compared to the `fetch` API. It's a standard. Standard don't go away that easily.

WebAssembly CG members representing four browsers, Chrome, Edge, Firefox, and WebKit.

backed with w3c
and its specs is backed by bcjcjccj.
As a side observation, the fact that all 4 major browser vendors have agreed to push it forward is probably a sogn that this tech has a bright future ahead.

backwards compatibility

## 2. There's "early" and "early"

When learning about Wasm, you might often read/hear the words "MVP" and "early". It is indeed a young technology.  
But it doesn't mean that it's not ready for production: it is.

<!-- It has been succesfully shipped before.  -->
<!-- Also its roadmap is solid. -->

## 3. No borders aka It's not just fast

Speed in the browser is certainly one solid benefit of WebAssembly. But it's only one part of the story.  
Because it's a compilation target and because it's highly portable, Wasm can transform:

- what apps we write // e.g. performance-demanding apps for the web
- how we write apps // e.g. write in C++ for the web
- where code run // e.g. a wasm module could run anywhere -> a way to universal libraries?

And many other rippled effects.

<!-- Wasm doesn't make assumptions about the environment it's running in.
- how you write it
- where it runs: everywhere
also it's a compilation target.
It is highly portable, which means in might. -->

<!-- Contrary to a new tool/framework, no matter how good:

- allows for incremental adoption
  A technology that is now supported by the most ubiquitous pieces fof software is here to stay.
- they know what they're doing
- it will permeate
  Wasm doesn't make assumptions about the environment it's running in - which is a powerful feature. -->

## 4. Under the hood

Understanding Wasm goes hand-in-hand with understanding how browsers execute JavaScript code - not just the event loop and the callback queue, but really how JS is transformed at runtime and run.  
After all, this is at the core of how web apps work, and worth having an idea about.

<!-- And isn't this the core of web development? -->

## 6. Good news

- not learn a new language

<!--
So if this is still a bit of a black box to you, Wasm will make this clearer. -->
