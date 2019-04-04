# // 🚧WIP

Machines and humans don't speak the same language.

- You write your code in a language you understand.
- What you wrote needs to be translated at some point into something the machine can understand.

Let's have a look at the spectrum of languages, between human and machines, and what they're good for.

## Human to metal

### Basics

Machine code = Native code ~= binary = the actual bytes (as instructions) that the CPU executes. Each machine code instruction causes the CPU to perform a very specific task: a load, a jump, or an ALU (arithmetic logic unit) operation on a unit of data in a CPU register or memory.
**Machine code depends on the machine's architecture.**
Example:

```javascript
1111; // in binary (base 2)
F; // same binary in hexadecimal i.e. base 16 (but still referred to "binary" as oversimplification). hexa is often used because it takes less space than binary, so errors are less likely.
```

High-level language = what language you write your code in ("source code"). A high-level language can be more or less high-level: for example, C++ is considered lower-level than JS, because you need to be a little more explicit about how you manage memory. We'll come back to that.
Example: JS, Rust

```javascript
const a = ' Hello ';
const b = a.trim();
```

Basic workflow:

- Write your code in C++
- Compile it ahead-of-time into a binary
- Give the binary to the machine, and let it run it.

### Now with VMs

Now that this is clear, let's have a look at how virtual machines fit in.  
Warning: this term is overloaded. What we'll talk about is not:

- VMs such as docker
- LLVM: it's more of a compile time VM.

Instead, we'll focus on runtime virtual machines.
Machine code is hardware-dependent.  
But because you don't want to target multiple physical architectures i.e. you want to be portable, you can instead add another layer. This layer is the virtual machine (VM): an abstraction over multiple kinds of machines.

VM usually refers to both:

- what runs your code
- facilities that are needed to run your code.

For example, V8 is an engine that can run JS code. Think of an engine as a specific kind of VM.  
V8 provides the event loop and other APIs needed by JS.  
NB: On top of that, comes the concept of the host - we'll touch on this later.

Example:

- SpiderMonkey, Chakra

### The last piece: Bytecode and Assembly language

Both are "intermediate languages" between source code and machine code.  
They're here for us humans to still be able to get a feeling for machine code ; they're not high-level, but human-readable. Language that is human-readable, but still closely associated with machine code instructions.

= ASM = "symbolic machine code" = "human-readable machine code"

Historically, the difference was:

- Bytecode targets a virtual machine (software)
- Assembly targets a specific CPU architecture / operating system.

Wasm is bytecode. You'll note that it's considered "assembly" even though it doesn't target a physical architecture, but a virtual machine. Wasm is a virtual assembly language. So, the line is a bit blurred±

https://techterms.com/definition/bytecode

`A* name$i`

## "Timing is everything"

So whenever you write code, it needs to be translated (= compiled) at some point into machine code.

_When_ this translation happens matters: it impacts the developer experience and how your program runs. Different approaches fit different use cases.

AOT. "AOT" really could be called AORT, ie ahead of Runtime.
Example:

- C++ is usually compiled down to binary
- LLVM-compiled WebAssembly. Note that in that case, there will be one more step at runtime: the JS/wasm engine will compile it to machine code and run it. We don't care yet whether Ignition or Turbofan or LiftOff will take care of it - the core idea is is that

If you don't compile it ahead of time:

- your destination needs to be able to compile it.
- your destination will need to compile it, which might take time

JIT
Example:

- Turbofan

Interpretation
...is usually not referred to as a compilation. But some compilation happens for sure!
If you ship JS to the browser, the engine will need at some point to translate it to machine code! So the interpreter also does some compilation.

## Flows

For example JS:

- you write JS // high-level
- JS is shipped as is over to the browser. In a compressed (gzipped), minified (uglified) format - but it's still text //
- The engine runs it:
  - The interpreter (Ignition) runs some portions, via its internal assembly. Note that this will also need to be compiled down to machine code at some point!
  - The optimizing compiler optimizes and runs hot portions.

## LLVM and compilers

backend frontend of a compiler  
immediate representation  
LLVM backend vs emscripten

## Wrapup: the browser

---

## Glossary/Disambiguations

- Executable: an overloaded term, that means "something the computer can run". It can be meant as actual machine code, or "anything you can run on the computer provided that the runtime is also installed", e.g. a Ruby or Rust script.
- Engine: a special kind of virtual machine.
- You might hear that "WebAssembly is a VM". What that means is that WebAssembly is a language that can run in a VM.

---

Sources:
https://en.wikipedia.org/wiki/Machine_code
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file
https://en.wikipedia.org/wiki/Executable
https://en.wikipedia.org/wiki/Assembly_language
https://en.wikipedia.org/wiki/Machine_code
