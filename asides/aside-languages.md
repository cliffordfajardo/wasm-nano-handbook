# // 🚧WIP 

Machines and humans don't speak the same language.  
- You write your code in a language you understand. 
- Then, that language is translated into something the machine can understand.

Let's have a look at the spectrum of languages, between human and machines, and what they're good for.

## Human to metal
### Basics 
Machine code = Native code ~= binary = the actual bytes (as instructions) that the CPU executes. Each machine code instruction causes the CPU to perform a very specific task: a load, a jump, or an ALU (arithmetic logic unit) operation on a unit of data in a CPU register or memory. 
**Machine code depends on the machine's architecture.** 
Example:
```javascript
1111 // in binary (base 2)
```

High-level language = what language you write your code in. A high-level language can be more or less high-level. C++ is considered lower-level than JS, because you need to be a little more explicit about how you manage memory, for example. We'll come back to that.
Example: JS, Rust
```javascript
const a = ' Hello ';
const b = a.trim();
```

Basic workflow: 
- Write your code in C++ 
- Compile it ahead-of-time into a binary
- Give the binary to the machine, and let it run it.

### With VMs
Now that this is clear, let's have a look at how virtual machines fit in.  
Machine code is hardware-dependent. Because you don't want to target multiple architectures, you can instead add another layer. This layer will
<!-- This all works based on the assumption that your VM -->

## When that translation happen

## Zoom on the browser

## Compilers 


## Terminology
* "Executable": an overloaded term, that means "something the computer can run". It can be meant as "machine code", or "anything I can run on the computer provided that the runtime is also installed", e.g. a Ruby or Rust script.
* Machine code: 
* Engine: a special kind of virtual machine.

## What's the point of stack machines?  
It's a model on how the code will be run. It's just another way to put it.

## Workflows
JS: 
- you write JS // high-level









## LLVM and compilers

backend frontend of a compiler    
immediate representation     
LLVM backend vs emscripten

## Code format

high-level language // middle-level (=C)// assembly language //// machine code  
<------------------------------------------------------------>
human-readable ----------------------------- not human-readable
high-level low-level
not executable by CPU executable by CPU
"source code"

### Machine code

= Native code ~= binary = the actual bytes (as instructions) that the CPU executes. Each machine code instruction causes the CPU to perform a very specific task: a load, a jump, or an ALU (arithmetic logic unit) operation on a unit of data in a CPU register or memory.
Example:
`1111` // in binary (base 2)
`F` // same binary in hexadecimal i.e. base 16 (but still referred to "binary" as oversimplification). hexa is often used because it takes less space than binary, so errors are less likely.

### Bytecode

= compiled code that targets a virtual machine (rather than a specific computer architecture). Contrary to binaries, bytecode isn't machine code.

But (!!! to check): it can look like it.
Example: xxxx todo

### Assembly language

= ASM = "symbolic machine code"

Language that is human-readable, but still closely associated with machine code instructions. Each assembly language (except WASM I think) is specific to a particular computer architecture and operating system. In contrast, most high-level programming languages are generally portable across multiple architectures but require interpreting or compiling.
NB: Bytecode and assembly language are similar: not high-level but readable ; both are "intermediate languages" between source code and machine code. Main difference: bytecode is generated for a virtual machine (software), while assembly language is created for a CPU (hardware). Src: https://techterms.com/definition/bytecode
Example:
A C compiler generates native machine code for a native machine architecture.
In the most common implementations, some python code (somefile.py) when imported creates a file (somefile.pyc) in the same directory; this is bytecode that will be run by the python VM. So python is semi-compiled (compiled invisibly).
There is yet another concept called JIT, where code is actually compiled to native machine code on the fly.
Also, there is interpreted: Ruby is no doubt an interpreted language since the source code is processed by an interpreter at the point of execution.

`A* name$i`

### High-level language

E.g. JS, Rust, ...  
Example:

```javascript
const a = ' Hello ';
const b = a.trim();
```

Workflow:
Programmer writes high-level language OR assembly language, that is then compiled to executable machine code (by a compiler or assembler, respectively).
NB: interpreted programs are an exception, they're not compiled to machine code.

Sources:
https://en.wikipedia.org/wiki/Machine_code
https://stackoverflow.com/questions/21571709/difference-between-machine-language-binary-code-and-a-binary-file
https://en.wikipedia.org/wiki/Executable
https://en.wikipedia.org/wiki/Assembly_language
https://en.wikipedia.org/wiki/Machine_code 


## Languages


| Language   | Type system                       |       Garbage-collected | Multi-threaded |   Cool | LLVM support |
| ---------- | :-------------------------------- | ----------------------: | -------------: | -----: | -----------: |
| C          | static, weakly typed              |                      no |            yes | -----: |       -----: |
| C++        | static, ~strongly typed (Generic) |                      no |            yes | -----: |       -----: |
| C#         | static, ~strongly typed           |                     yes |            yes | -----: |       -----: |
| python     | dynamic, ~strongly typed          | yes (ref counting + GC) |            yes | -----: |       -----: |
| Java       | static, strongly typed            |                     yes |            yes | -----: |       -----: |
| JavaScript | dynamic, weakly typed             |                     yes |            yes | -----: |       -----: |
| Rust       | static, strongly typed            |          no (Ownership) |            yes | -----: |       -----: |
| wasm       | static, strongly typed            |              no, coming |            yes | -----: |       -----: |



* statically typed language: each variable's type is determined at compile time and not run-time 
* strongly typed: the language is strict about what should be typed ; ( (the interpreter keeps track of all variables types)
