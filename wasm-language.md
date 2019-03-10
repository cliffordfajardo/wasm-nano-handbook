ℹ️ _This is raw content, just the core ideas - would need to be reshaped for a more engaging reading experience._  

----

# WASM is a stack machine

WASM is a STACK MACHINE language. 

* A **stack** is a LIFO (last in first out) data structure that has two operations: push and pop.
* A **stack machine**  is a stack for which items are instructions, which run and evaluate, and push and pop values on this stack.

WebAssembly only supports 4 types - 2 integer types and 2 floating point types. To model strings you share the same piece of linear memory - memory that can read from and write to from both WebAssembly and JavaScript.

Stack is a LIFO data structure that has 2 operations: push things onto the stack, or pop them off the stack.
e.g.: a call stack

Src: https://www.youtube.com/watch?v=6Y3W94_8scw Demystifying web assembly

# Core concepts

https://webassembly.github.io/spec/core/intro/introduction.html#design-goals ++++ and  
https://webassembly.github.io/spec/core/intro/overview.html ++++

# WASM flavors / representations

- Binary format // https://webassembly.github.io/spec/core/binary/index.html
- Text format = WAT. s-expressions, flat syntax, or mixed // https://webassembly.github.io/spec/core/text/index.html
  ...which one is the assembly?

WebAssembly modules are distributed in a binary format.  
Decoding processes that format and converts it into an internal representation of a module.
In the spec, this representation is modelled by abstract syntax, but a real implementation could compile directly to machine code instead.

Binary opcode:
0x6a (= add operation)

for wasm it looks like:

(Stack representation:
Just for us to understand

```
i32.const 1
i32.const 2
i32.add
call $log
```

"add 1 to the stack, add 2 to the stack, call add (add takes 2 args, by just popping them off the stack), push the result on the stack"

)

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

text representation = WAT = assembly:

If you’re writing code to run directly on a microprocessor, the instruction that the processor understands is a low-level machine code; bytes and so on.
3:06 Most assembly languages will have a slightly more readable version - the assembly language. You’ll have opcodes being represented as mnemonics instead of bytes. So the text format you see for WASM is just a more human version of the binary format which is the underlying WASM itself. It’s a very light syntactic sugar - there’s almost a 1-1 mapping between the text format and the binary format.
https://www.infoq.com/podcasts/colin-eberhardt-webassembly

```javascript
(local i32 i64)
  get_global 0
  i32.const 96
  i32.sub
  tee_local 2
  set_global 0
  get_local 2
  i32.const 8
  i32.add
  i32.const 16
  i32.add
```
