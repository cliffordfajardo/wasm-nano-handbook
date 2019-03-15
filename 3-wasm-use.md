 # Usage modes today - from a developer's perspective // 🚧WIP
 
 _On how to get started with Wasm as a developer, depending on your context._  
 _Up Next: [Wasm for the Web](https://github.com/maudnals/wasm-nano-handbook/blob/master/4-wasm-web.md)_

<p align="center">
<img width="520" src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/use.jpg">   
 	<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

---  

## Main usage modes
1. Use as dependency
2. Accelerate hot code portions of ordinary JS apps 
3. Develop for the web in the developers' language of choice
4. Deliver existing applications over the web, such as games / 3D Graphics
5. Others: see wasmer with docker use case + iOT // TBD

## Modes 1 and 2: example of a JS/TS app  
 
<p align="center">
<img src="https://raw.githubusercontent.com/maudnals/wasm-nano-handbook/master/img/wasm-use-case.png"> 
<div align="center"><sub><sup>©maudnals</sup></sub></div> 
</p>

### Wasm (Mode 1)   
Update your dependencies to replace them by Wasm modules when available.  
In theory if the API doesn't change, there's no work to do on your side. One example of that could be the React team updating their reconciliation algo to use Wasm.   
Benefits: 
* A smaller, faster codebase 

### Wasm (Mode 2)
Actually rewrite some hot code portions of yours in Wasm.  
Benefits: 
* An even smaller, faster codebase  
* More dev resources can be allocated to the codebase, and the team can grow heterogeneous, emulating cross-learning.  

### Get started
* Examples in prod: TBD
* Tutorials: TBD
* Mode 1: npm packages (+ all the hidden ones) 
* Mode 2: TBD. Refer to section 3 to see with languages are supported. 


## 3    

What languages can be compiled to Wasm today?    
Most of them - but with different levels of maturity.    
The ones that are static and LLVM are best supported for now. 

* C, C++:  highly mature, because it was used throughout the development of WASM and asm.js.
* Rust: gaining maturity rather quickly, because the nature of Rust makes it easy to target Wasm, e.g. Rust’s ownership model
* Java and C# (and JavaScript as well) still need a garbage collector. The way this works today, is that they take compile their GC to Wasm, and ship everything to the app page ; still experimental though.

Alternatively:    
* Experimental support:
  * Turboscript
  * TypeScript 
  * Walt
* Code in `.wat` directly.    

Note: This will evolve. You might be able to write Wasm from TypeScript someday!

### Get started
* C, C++: Emscripten // TBD add links 
* Rust: stdweb or bindgen, parcel wasm hasher // TBD add links 

## 4 
Mostly with C++.  


<div align="center"><sub><sup>©maudnals</sup></sub></div>
