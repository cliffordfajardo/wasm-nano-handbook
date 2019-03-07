# # 1 Back to basics

## CPU and GPU

CPU = central processing unit.

A CPU is good at doing complex manipulations on a small set of data.  
A GPU is good at doing simple manipulations on a large set of data.

MacBook pro CPU = 3.8GHz (= CPU clock speed = how much work a processor can do in a certain time. 1GHz = 1 billion bits per second, and # of cores = how many bits can be processed at once. Dual core 2.2 GHz can process 4.4 billion bits per second).

How a GPU works: it's a special kind of CPU, designed to perform SIMD = Single Instruction, Multiple Data. It's more efficient because less instruction-decoding overhead. But because large blocks are used, there are more parallel processing units, so a single GPU instructions uses more transistors (=> more space and energy needed, more heat is generated).

Only GPU is very good at data-parallel computing (and CPU is good at parallel processing, i.e. having many programs open at once).

Source: https://superuser.com/questions/308771/why-are-we-still-using-cpus-instead-of-gpus

## CPU, GPU and RAM

The RAM is a temporary storage area from which retrieval is faster than from disk / permanent storage.
When the CPU needs to process some data, the data will be first loaded onto the RAM so that the CPU can retrieve it faster, which will speed things up alltogether. CPU is the brain, RAM is the book, permanent storage is the bookshelf.
NB: GPU also uses RAM, new systems have GPU integrated in the CPU.
Source: https://superuser.com/questions/78362/what-is-the-relationship-between-cpu-usage-and-ram

## Code format

high-level language //// assembly language //// machine code  
<------------------------------------------------------------>
human-readable ----------------------------- not human-readable
high-level low-level
not executable by CPU executable by CPU
"source code"

**Machine code**  
= Native code ~= binary = the actual bytes (as instructions) that the CPU executes. Each machine code instruction causes the CPU to perform a very specific task: a load, a jump, or an ALU (arithmetic logic unit) operation on a unit of data in a CPU register or memory.
Example:
`1111` // in binary (base 2)
`F` // same binary in hexadecimal i.e. base 16 (but still referred to "binary" as oversimplification). hexa is often used because it takes less space than binary, so errors are less likely.

**Bytecode**  
= compiled code that targets a virtual machine (rather than a specific computer architecture). Contrary to binaries, bytecode isn't machine code. Example: xxxx todo

**Assembly language** = ASM = "symbolic machine code"
Language that is human-readable, but still closely associated with machine code instructions. Each assembly language (except WASM I think) is specific to a particular computer architecture and operating system. In contrast, most high-level programming languages are generally portable across multiple architectures but require interpreting or compiling.
NB: Bytecode and assembly language are similar: not high-level but readable ; both are "intermediate languages" between source code and machine code. Main difference: bytecode is generated for a virtual machine (software), while assembly language is created for a CPU (hardware). Src: https://techterms.com/definition/bytecode
Example:
A C compiler generates native machine code for a native machine architecture.
In the most common implementations, some python code (somefile.py) when imported creates a file (somefile.pyc) in the same directory; this is bytecode that will be run by the python VM. So python is semi-compiled (compiled invisibly).
There is yet another concept called JIT, where code is actually compiled to native machine code on the fly.
Also, there is interpreted: Ruby is no doubt an interpreted language since the source code is processed by an interpreter at the point of execution.

`A* name$i`

**High-level language**: javascript, rust, ...
Example:
`const a = " Hello "; const b = a.trim();`

Workflow
Programmer writes high-level language OR assembly language, that is then compiled to executable machine code (by a compiler or assembler, respectively).
NB: interpreted programs are an exception, they're not comnpiled to machine code.

NB:
Executable = something the computer can run.
Can be meant as...
Machine code // 01010100100001
OR
"anything I can run on the computer provided that the runtime is also installed" // e.g. a ruby or rust script.

Sources:
https://en.wikipedia.org/wiki/Machine_code
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file
https://en.wikipedia.org/wiki/Executable
https://en.wikipedia.org/wiki/Assembly_language
https://en.wikipedia.org/wiki/Machine_code

- Web dev accessible to all developers

# What is WASM

## Where it comes from

## What is WASM

WASM is an efficient, low-level assembly-like language / bytecode (source: mdn).
Core principles:

- performance // almost-native-speed
- safe // no memory overflow
- portable // it's a compilation target
- backward compatibility

## How to write WASM

WASM is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

## How it works

## Why WASM is faster

Fast to load and parse and execute
VM

## WASM language

It's a stack machine language. A stack is a datas structure that has two operations: push and pop. It's LIFO order (last in first out).
A stack machine is a stack for which items are instructions, which run and evaluate and push and pop values on this stack.

## WASM flavors / representations

Stack representation:

```
i32.const 1
i32.const 2
i32.add
call $log
```

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
3:06 Most assembly languages will have a slightly more readable version - the assembly language. You’ll have opcodes being represented as mnemonics instead of bytes. So the text format you see for WASM is just a more human version of the binary format which is the underlying web assembly itself. It’s a very light syntactic sugar - there’s almost a 1-1 mapping between the text format and the binary format.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## Why it will change the world

# WASM use cases

# WASM ecosystem/flavours

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

---

# Challenges of WASM

# Future of WASM

# Disambiguations

## WASM vs WebGL?

They are rather unrelated, but can be used together.

WebGL is a browser's API onto the machine's GPU (= graphical processing unit = 3D hardware). It's based on the OpenGL standard.

Web developers can use JS/WASM/... to access WebGL when they need to do 3D graphics fast.

More: https://getpocket.com/a/read/2365657803

## GPU, CPU, WASM

## WASM vs ASM

ASM is a mozilla-built PoC of a low-level virtual machine out of JavaScript. They took a very strict subset of the language, and like web assembly they have the concept of memory being an array. They defined their own language, on top of JavaScript. They built into their own browser something that understood the language they’d created, and optimised for it. The whole thing was a very clever and slightly crazy experiment, but it worked.

ASM and WASM are similar - they define an assembly-like set of instructions.
Problems of ASM.js:

- it is coded in JavaScript so is quite verbose and difficult to understand syntax.
- In addition, it is only optimised for Firefox (?).
  In hind-sight, it looks like a very early proof of concept for web assembly.

https://www.infoq.com/podcasts/colin-eberhardt-webassembly

## How is web assembly different from writing, say, Flash?

3:35 Part of the reason why people think it sounds similar is because one of the motivations of creating web assembly is to create a new assembly language which is a compilation target for a range of high level languages.
3:50 So C#, Java, Rust, C++ and others are now able to be compiled into web assembly and run in the browser.
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

# Tools & Resources

## Tools

https://mbebenita.github.io/WasmExplorer/
https://webassembly.studio/

## Curated list

https://github.com/mbasso/awesome-wasm

## Benchmarks

https://pspdfkit.com/blog/2018/a-real-world-webassembly-benchmark/
https://medium.com/@torch2424/webassembly-is-fast-a-real-world-benchmark-of-webassembly-vs-es6-d85a23f8e193
https://lemire.me/blog/2018/10/23/is-webassembly-faster-than-javascript/

# Misc

A cute feature of the logo is that the notch in the top enables it to connect with the JavaScript logo.

# Inbox

### ASM, AST
