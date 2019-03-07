---

# Back to basics

---

## CPU vs GPU

CPU = central processing unit
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

high-level language assembly language machine code \* \* \*
<------------------------------------------------------------>
human-readable not human-readable
high-level low-level
not executable by CPU executable by CPU
"source code"

**Machine code** = Native code ~= binary = the actual bytes (as instructions) that the CPU executes. Each machine code instruction causes the CPU to perform a very specific task: a load, a jump, or an ALU (arithmetic logic unit) operation on a unit of data in a CPU register or memory.
Example:
`1111` // in binary (base 2)
`F` // same binary in hexadecimal i.e. base 16 (but still referred to "binary" as oversimplification). hexa is often used because it takes less space than binary, so errors are less likely.

**Bytecode** = compiled code that targets a virtual machine (rather than a specific computer architecture). Contrary to binaries, bytecode isn't machine code. Example: xxxx todo
**Assembly language** = asm = "symbolic machine code" = language that is human-readable, but still closely associated with machine code instructions. Each assembly language (except wasm I think) is specific to a particular computer architecture and operating system. In contrast, most high-level programming languages are generally portable across multiple architectures but require interpreting or compiling.
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

---

# Browser, engine and wasm

---

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

# Wasm

---

### What is wasm

Wasm is an efficient, low-level assembly-like language / bytecode (source: mdn).
Core principles:

- performance // almost-native-speed
- safe // no memory overflow
- portable // it's a compilation target
- backward compatibility

### How to write wasm

wasm is low-level, so rust and C++ are easy to compile to rust: they're medium-level, and don't need garbage collection.

### How it works

### Why wasm is faster

Fast to load and parse and execute
VM

### wasm language

It's a stack machine language. A stack is a datas structure that has two operations: push and pop. It's LIFO order (last in first out).
A stack machine is a stack for which items are instructions, which run and evaluate and push and pop values on this stack.

### wasm flavors / representations

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

### Asm, AST

### Wasm vs WebGL?

WebGL is a browser's API onto the machine's GPU ( = graphical processing unit = 3D hardware). It's based on the OpenGL standard.
Web developers can use JS/wasm/... to access WebGL when they need to do 3D graphics fast.

More: https://getpocket.com/a/read/2365657803

### GPU, CPU, wasm?????
