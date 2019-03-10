ℹ️ _This is raw material - can be reshaped into publishing material for a more engaging reading experience._  

----

## WASM core concepts

1) WASM is a **stack machine** language.  
* A stack is a LIFO (last in first out) data structure that has two operations: push and pop.
* A stack machine is a stack for which items are instructions, which run and evaluate, and push and pop values on this stack. e.g.: a call stack.  

Basic stack example:
```wasm
i32.const 1 // Add 1 to the stack
i32.const 2 // Add 2 to the stack
i32.add // Call add, that takes 2 args, by just popping them off the stack
call $log // Push the result on the stack"
```

2) WASM only supports **4 types**.   
2 integer types and 2 floating point types.  
To model strings, one would share the same piece of linear memory ; for example in the web, memory that can be read from and written to from both WASM and JS.  

3) Code is organized into separate **functions**.    

4) A WASM binary takes the form of a **module**.  
With import/export functionalities, and can also define a start function that is automatically executed. 

5) A WASM implementation will typically be embedded into a **host environment**.   
This environment defines how loading of modules and import/exports work. 

More:  
* https://www.youtube.com/watch?v=6Y3W94_8scw Demystifying web assembly
* https://webassembly.github.io/spec/core/intro/introduction.html#design-goals 
* https://webassembly.github.io/spec/core/intro/overview.html ++++  

## WASM flavors / representations   

### Binary format (`.wasm`)

### Text format (`.wat`) 




ast? 

Assembly


- Binary format // https://webassembly.github.io/spec/core/binary/index.html
- Text format = WAT. s-expressions, flat syntax, or mixed // https://webassembly.github.io/spec/core/text/index.html
  ...which one is the assembly?

WebAssembly modules are distributed in a binary format.  
Decoding processes that format and converts it into an internal representation of a module.
In the spec, this representation is modelled by abstract syntax, but a real implementation could compile directly to machine code instead.

Binary opcode:
0x6a (= add operation)

for wasm it looks like:






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
