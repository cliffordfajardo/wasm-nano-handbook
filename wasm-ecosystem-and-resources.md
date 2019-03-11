## Who is Wasm?

The WebAssembly team includes people from Google, Microsoft, Mozilla, Apple, and others under the banner of the W3C WebAssembly Community Group.

## Wasm official projects

- binaryen: compiler infrastructure and toolchain library for WebAssembly, in C++
- wasm-jit-prototype: standalone VM using LLVM JIT
- design: WebAssembly Design Documents 
- wabt: The WebAssembly Binary Toolkit // https://github.com/WebAssembly/wabt is a suite of tools for WebAssembly, including:
  - wat2wasm: translate from WebAssembly text format to the WebAssembly binary format
  - wasm2wat: the inverse of wat2wasm, translate from the binary format back to the text format (also known as a .wat)
  - wasm-objdump: print information about a wasm binary. Similiar to objdump.
  - wasm-interp: decode and run a WebAssembly binary file using a stack-based interpreter
  - wat-desugar: parse .wat text form as supported by the spec interpreter (s-expressions, flat syntax, or mixed) and print "canonical" flat format
  - wasm2c: convert a WebAssembly binary file to a C source and header
  - wasm-strip: remove sections of a WebAssembly binary file
  - wasm-validate: validate a file in the WebAssembly binary format
  - wast2json: convert a file in the wasm spec test format to a JSON file and associated wasm binary files
  - wasm-opcodecnt: count opcode usage for instructions
  - spectest-interp: read a Spectest JSON file, and run its tests in the interpreter 
  
# Core/Official

* https://webassembly.github.io/spec/core/intro/overview.html ++++
* https://webassembly.org/

# Curated lists

* https://github.com/mbasso/awesome-WASM
* https://github.com/appcypher/awesome-wasm-langs#haskell 

# Tools

* https://mbebenita.github.io/WasmExplorer/
* https://webassembly.studio/

# Benchmarks

* https://pspdfkit.com/blog/2018/a-real-world-webassembly-benchmark/
* https://medium.com/@torch2424/webassembly-is-fast-a-real-world-benchmark-of-webassembly-vs-es6-d85a23f8e193
* https://lemire.me/blog/2018/10/23/is-webassembly-faster-than-javascript/

