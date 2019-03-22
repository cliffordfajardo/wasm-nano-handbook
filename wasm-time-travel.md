## Time travel

### The past - Recent history of Wasm 🚧WIP

- 2015: Wasm community group
- 2017: cross-browser consensus
- 2018: draft of the specification 1.0: core spec (=syntax, naming, building, validayion, execution + the standard for the binary format ie types and values), JS interface (interactions between Wasm modules and JS, data storage, sandboxing), web API (rules about module compilation and interactions between the dom and the Wasm modules).

### Wasm today 🚧WIP

- Wasm 1.0 is an MVP, that has shipped in 4 major browser engines.
- It is still early stage: no native strings nor exception handling ; these can be emulated within the basic Wasm but the resulting code is slow. Also, interop between for example JS and Wasm is still complex (calling functions is easy, but it’s the types to send back and forth that is the challenge)
  https://www.i-programmer.info/news/98-languages/10563-webassembly-is-ready-for-use.html

_Up Next: [The Language](https://github.com/maudnals/wasm-nano-handbook/blob/master/2-wasm-language.md)_

### Future of Wasm 🚧WIP

### Future

#### Near

Features planned for Wasm 2.0:

- multi-threading model and garbage collection // C# and Java support will become easier
- multi-value returns
- host binding // JS objects will be more easily exposed to Wasm

#### Distant

https://medium.com/javascript-scene/why-we-need-webassembly-an-interview-with-brendan-eich-7fb2a60b0723

Once all the browsers support both Wasm and ASM.js, Wasm can start to grow extra semantics that need not be put into JS.
They may in fact be put into both JavaScript and Wasm because it’s the same one engine (1vm). But there are certain things we might not want to ever put into JS that could be put into Wasm:

- shared memory array buffers to get multi-threaded games. Too complicated for JS: risk for race conditions in JavaScript, fragile process with bug hazards
- zero cost exceptions might not make sense in JavaScript. They require some compiler and runtime cleverness, but they do make sense for C++, and Swift. Might benefit other languages like C++ or Haskell
- call/cc (call-with-current-continuation). Call/cc is too powerful a tool. It has challenges for JS engines in implementation and security hazards. You have these non-local functional gotos. You can call a continuation and be off in a different stack. So it’s not like the local, limited continuations like we have in generators in ES6. It’s a deeper continuation. So call/cc could be put into Wasm, into the engine that handles both Wasm and JavaScript down the road.
