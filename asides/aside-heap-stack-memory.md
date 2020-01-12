# Memory in JS

Sources:

* https://hashnode.com/post/does-javascript-use-stack-or-heap-for-memory-allocation-or-both-cj5jl90xl01nh1twuv8ug0bjk
* Interview Cake
$ * Rust book

## The stack and the heap

Both the stack and the heap are regions in the RAM (where the computer stores variables at runtime).

### Stack

<p align="center">
<img width="520" src="https://images-na.ssl-images-amazon.com/images/I/71Ap7cgEglL._SX466_.jpg">  
  <div align="center"><sub><sup>Stack</sup></sub></div>
</p>

Memory set aside **as scratch space for the execution thread**.
It's **thread-specific** and operates in LIFO. When a new thread is started by a computer program (usually the main thread first), a new stack is created.

✅ Upsides:

* Very fast access (it's a stack: the place to access new data is always the top);
* No explicit deallocation needed (when a function exits its variables are popped off the stack);
* Efficient space management by the CPU.

❌ Drawbacks:

* Limited size;
* Local variables only;
* No variable resizing is possible.

=> Use to **quickly/temporary store/retrieve simple data** (primitives: integer, float, pointer which is just an integer).

### Heap

<p align="center">
<img width="520" src="https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwjksYLht_7mAhUMCxoKHejACUEQjRx6BAgBEAQ&url=https%3A%2F%2Fwww.masterfile.com%2Fsearch%2Fen%2Fpaper%2Bdump&psig=AOvVaw26zqku0CtE08UZGMOTYFNR&ust=1578931332460627">  
  <div align="center"><sub><sup>Heap</sup></sub></div>
</p>

Memory set aside **for dynamic allocation**.
It's **app-specific**. "Allocating" means on the heap (e.g. `new` keyword in C)

✅ Upsides:

* More space (virtual memory can be used).

❌ Drawbacks:

* Storing/Accessing is a lot slower (because a lot of bookkeeping + despite optimizations, data is fragmented and unordered);
* Must manage manually to prevent memory leaks.

=> Use to store arbitrary data in an unordered fashion, when long lifetime is needed, or large data, or data size unknown.

NB: In order to quickly find heap-data when doing operations, a pointer to it is stored on the stack.

## V8 and memory

V8 has a heap and a stack.
JS' ECMA-262 standard does not define memory layout, so whatever V8 uses depends on how the interpreter is implemented.

JS is garbage-collected: there is data scattered around which has to be cleaned up. Does that sound like the data is stored on the stack? No, because the stack has strictly ordered data.

**So, in V8 variables are allocated on the heap.**
V8's C++ **STORES data structures on the HEAP** and **works with pointers to it in the STACK**.

What's interesting is what the optimizer does later on: if a variable is always used as a boolean, it might as well drop the structure and use it as a boolean on the stack.

The stack for storing objects is the same as the runtime call stack. It records where in the program we are, keeps track of execution contexts (stack frames). If we step into a function we push a new frame onto the stack, if we return we pop off it. In V8 there's just ONE stack because one thread => one call stack.

One stack frame = all the data for one function call (gets popped off the stack when the function returns) =

* parameters e.g. pointers to the heap;
* local variables including stack-allocated objects;
* return address: which code to run after the function returns.

V8 has:

* A (call) stack // to keep track of the execution contexts, and potentially stores variables that the optimizer knows are always of the same type;
* A heap // to allocate memory. Because if the stack has to much stuff on it, it's stuck and that freezes the UI, we don't want that.

Note it doesn't really matter because:

JS is a dynamic language and as such memory allocation happens dynamically.
JS has loose typing which generally makes it less useful to keep data on the stack. I'm sure the VM uses the stack when it sees fit though.
The stack and heap concept stem from the early days of processors when memory was more or less statically allocated and the stack was typically accessed using a fast 1 opcode instruction as opposed to 3-4 opcodes for a heap or direct memory access. Modern CPU architectures work differently and don't really make a huge difference between stacks and heaps. As long as there is no cache-miss, performance difference should be minor if not negligible. In reality it comes down to how good or bad the the VM is at realtime optimisation and memory management.
