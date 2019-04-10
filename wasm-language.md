# Language // 🚧WIP

_On how Wasm code looks, feels, and executes.
Before digging into this chapter: if you're a bit rusty on what "machine language" vs. "high-level language" mean, check out (TBD add link)._

_↠ Up Next: [Usage modes](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-use.md)._

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/language.jpg">   
	<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

[1. Wasm is Assembly ](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-language.md#wasm-is-assembly)  
[2. Wasm is a stack machine](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-language.md#wasm-is-a-stack-machine)  
[3. Two shapes](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-language.md#two-shapes)  
[4. Module](https://github.com/maudnals/wasm-nano-handbook/blob/master/wasm-language.md#module)

---

## ⚡ TL;DR

Wasm looks very different from JS. What makes it different is also what makes it fast.  
But you don't need to be able to write Wasm directly to benefit from it.

## Where

## Wasm is Assembly

💡 [What is Assembly?](https://github.com/maudnals/wasm-nano-handbook/blob/master/asides/aside-languages.md)

Basics:

- Assembly is "symbolic machine code" i.e. human-readable.
- Assembly code normally depends on the machine type But when delivering code on a user's machine across the web, we don't know what the target architecture will be. So, Wasm is a special assembly: **it's a machine language for a VM**.
- Wasm is a rather simple kind of Assembly.

// TBD add schema + source.

## Wasm is a stack machine language

Because Wasm is low-level, the way it's represented should be closer to how machines run code. Two commons approaches for this are registers and stack machines.

Wasm's execution is represented as a **stack machine**.

- A **stack** is a LIFO (last in first out) data structure. It has two operations: push and pop.
- A **stack machine** is a stack for which items are **instructions**. Each instruction and pushes and pops values to/from this stack. e.g.: a call stack.

But remember: wasm is virtual assembly code. It means that the host environment, e.g. the browser, will compile it to machine code at runtime. So going back to our stack representation: it's just a representation. Under the hood when wasm code is run, registers will be used.

Basic stack example:

// TBD add illustration

```wasm
i32.const 1 // Add 1 to the stack
i32.const 2 // Add 2 to the stack
i32.add // Call add, that takes 2 args, by just popping them off the stack
call $log // Push the result onto the stack"
```

**What's the point of stack machines?**
It's a model to run your code against.

## Wasm core concepts

1. A Wasm implementation will typically be embedded into a **host environment**.  
   This environment defines how loading modules and import/exports work.

2. A Wasm binary takes the form of a **module**, that has:

- Function: index of functions defined in this module
- Type: functions signatures defined in thie module
- Code: the actual function bodies
- Import/export functionalities
- Can also define a start function that is automatically executed.

3. Code is organized into separate **functions**.

4. Wasm supports **4 types**.

   - 2 integer types
   - 2 floating point types.  
     To model strings, one would share the same piece of linear memory ; for example in the web, memory that can be read from and written to from both Wasm and JS.

More:

- https://www.youtube.com/watch?v=6Y3W94_8scw Demystifying web assembly
- https://webassembly.github.io/spec/core/intro/introduction.html#design-goals
- https://webassembly.github.io/spec/core/intro/overview.html ++++

## Two shapes

- "Binary" format: for the VM
- Text format: for humans

### "Binary" format: .wasm

"Binary" ... actually hexa
"Dense linear encoding of the abstract syntax" i.e. efficient form of binary that allows for fast decoding, small file size, and reduced memory usage.  
Good for: network transfer, use by JS engine (which will only need to decode it).

```wasm
... TBD
```

Opcodes are represented as bytes, e.g.:
`0x6a` // add operation.

Remember: Assembly code (e.g. Wasm) is VM-specific.

### Text format: .wat

.wat is the human-readable form of .wasm. It’s a light syntactic sugar ; the text format and the binary format map almost 1:1.  
Good for: humans.

E.g. source maps (browsers display "wasm" but it reality what you see is "wat")

```
(call $log
	(i32.add
		(i32.const 1)
		(i32.const 2)
	)
)
```

- Code is represented with S-expressions, a format that represents trees well. Note that a Wasm tree is rather flat.
- Opcodes (= operation codes = the ID of an operation) are represented with mnemonics i.e. human-redable names instead of bytes.

More: https://developer.mozilla.org/en-US/docs/WebAssembly/Understanding_the_text_format

### The abstract syntax tree (AST)

... is not a format in itself. It's the "underlying logic" of the code.
.wat and .wasm both map 1-1 to the abstract syntax tree.

## Module

A module is Wasm's fundamental unit of code.

A module is the "distributable, loadable, and executable unit of code in WebAssembly" - the packaged version, if you will.
At runtime, a module can be instantiated with a set of import values to produce an instance.

WebAssembly modules are distributed in a binary format.  
Decoding processes that format and converts it into an internal representation of a module.
In the spec, this representation is modelled by abstract syntax, but a real implementation could compile directly to machine code instead.

Sources:

- https://hub.packtpub.com/the-elements-of-webassembly-wat-and-wasm-explained-tutorial/
- https://www.youtube.com/watch?v=6Y3W94_8scw
- https://www.infoq.com/podcasts/colin-eberhardt-webassembly
  More details:
- https://hub.packtpub.com/the-elements-of-webassembly-wat-and-wasm-explained-tutorial/
- https://webassembly.github.io/spec/core/binary/index.html
- https://webassembly.github.io/spec/core/text/index.html
