## Wasm is assembly

Also see: https://github.com/maudnals/wasm-nano-handbook/blob/master/basics-language-to-machine.md

Recall:
* Assembly is "symbolic machine code" ie human readable. 
* Assembly code depends on the machine type 

When delivering code on a user's machine across the web, we don't know what the target architecture will be. So, Wasm is a special assembly: it's a machine language for a virtual machine.
// here add schema. 



## WASM core concepts

1) WASM is a **stack machine** language.  
* A stack is a LIFO (last in first out) data structure that has two operations: push and pop.
* A stack machine is a stack for which items are instructions, which run and evaluate, and push and pop values on this stack. e.g.: a call stack.  

Basic stack example:
```wasm
i32.const 1 // Add 1 to the stack
i32.const 2 // Add 2 to the stack
i32.add // Call add, that takes 2 args, by just popping them off the stack
call $log // Push the result onto the stack"
``` 

WASM implements a stack-machine ; it is a virtual stack and not the program stack.

2) WASM supports **4 types**.   
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

## WASM shapes    

* "Binary" format: for the VM 
* Text format: for humans 

### Binary format: .wasm  

"Dense linear encoding of the abstract syntax" i.e. efficient form of binary that allows for fast decoding, small file size, and reduced memory usage.  
Good for: network transfer, use by JS engine (which will only need to decode it).

```wasm
reduce_sum_u8reduce_sum_u8_vec
rgbas_to_rgbsavg_vec_f64avg_rgb_f64__web_malloc-
__web_free.__web_tablememory__heap_base
__data_end	DA4�&#18<*254)('MFKIJCHUVGB�bchegv}�x�ynz������
���#A�k"$ A8jAj Aj)7 A8jAj Aj)7  )78@@ -8AG 
``` 
Opcodes are represented as bytes, e.g.:
`0x6a` // add operation. 

Remember: Assembly code (e.g. WASM) is VM-specific.

### Text format: .wat
.wat is the human-readable form of .wasm. It’s a light syntactic sugar ; the text format and the binary format map almost 1:1.  
Good for: humans. E.g. source maps (browsers display "wasm" but it reality what you see is "wat")
```
(call $log
	(i32.add
		(i32.const 1)
		(i32.const 2)
	)
)
```   
* Opcodes are represented as mnemonics instead of bytes.
* S-expressions are used. Code written in s-expressions can be concisely expressed in a tree structure, which is why s-expressions were chosen for WebAssembly’s text format.  


### The abstract syntax tree (AST)
... is not a format in itself.  It's the "underlying logic" of the code.
.wat and .wasm both map 1-1 to the abstract syntax tree.

### Module 
A module is the "distributable, loadable, and executable unit of code in WebAssembly" - the packaged version, if you will. 
At runtime, a module can be instantiated with a set of import values to produce an instance.

WebAssembly modules are distributed in a binary format.  
Decoding processes that format and converts it into an internal representation of a module.
In the spec, this representation is modelled by abstract syntax, but a real implementation could compile directly to machine code instead.


Sources:  
* https://hub.packtpub.com/the-elements-of-webassembly-wat-and-wasm-explained-tutorial/
* https://www.youtube.com/watch?v=6Y3W94_8scw  
* https://www.infoq.com/podcasts/colin-eberhardt-webassembly
More details: 
* https://hub.packtpub.com/the-elements-of-webassembly-wat-and-wasm-explained-tutorial/
* https://webassembly.github.io/spec/core/binary/index.html
* https://webassembly.github.io/spec/core/text/index.html
