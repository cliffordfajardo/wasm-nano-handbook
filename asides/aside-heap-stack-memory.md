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
* Efficient space management by the CPU

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

JS' ECMA-262 standard does not define memory layout, so whatever V8 uses depends on how the interpreter is implemented.

JS is a garbage-collected language; this means that there is data scattered around which has to be cleaned up. Does that sound like the data is stored on the stack? Rather... no, because the stack has strictly ordered data.
So, in V8 variables are allocated on the heap.

The most direct way to find out how V8 handles things so is to take a look at the actual source code (hooray for opensource!). In order to find out the basic data type, I used the NodeJS unofficial V8 reference, and looked up how to pass a Boolean value around inside V8. In order to do so, a class called "Boolean" is used. Whenever I use a boolean value, that class is instantiated. Well, basically that's C++ land. C++, like C, stores data structures on the heap and only works with pointers to it in the stack. So, whenever V8 has to allocate a new variable, it allocates a structure holding the data plus additional information on the heap (so much for the answer to your original question). What's interesting is what the optimizer does later on, because if a variable is always used as a boolean, it might as well drop the structure and use it as a boolean on the stack, which would bring us to system-performance without all that soft abstraction stuff on top.

TBD

V8 has:

* A (call) stack // It records where in the program we are, keeps track of execution contexts (stack frames). If we step into a function we push a new frame onto the stack, if we return we pop off it. In V8 there's just one stack because one thread => one call stack.
* A heap // for memory allocation. If the stack has stuff on it, it's stuck. We don't want that, that freezes the UI.


The stack and heap concept stem from the early days of processors when memory was more or less statically allocated and the stack was typically accessed using a fast 1 opcode instruction as opposed to 3-4 opcodes for a heap or direct memory access. Modern CPU architectures work differently and don't really make a huge difference between stacks and heaps. As long as there is no cache-miss, performance difference should be minor if not negligible. In reality it comes down to how good or bad the the VM is at realtime optimisation and memory management.

JS allocates everything on the heap in order to run GC on the memory regions easily.

Heap has to be garbage-collected



The simple answer is: Heap. But it doesn't really matter because:

JS is a dynamic language and as such memory allocation happens dynamically.
JS has loose typing which generally makes it less useful to keep data on the stack. I'm sure the VM uses the stack when it sees fit though.
The stack and heap concept stem from the early days of processors when memory was more or less statically allocated and the stack was typically accessed using a fast 1 opcode instruction as opposed to 3-4 opcodes for a heap or direct memory access. Modern CPU architectures work differently and don't really make a huge difference between stacks and heaps. As long as there is no cache-miss, performance difference should be minor if not negligible. In reality it comes down to how good or bad the the VM is at realtime optimisation and memory management.
