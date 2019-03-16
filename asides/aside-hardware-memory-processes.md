# Basics of Hardware, Memory, and Processes // 🚧WIP


## CPU and GPU

CPU = central processing unit.

A CPU is good at doing **complex manipulations** on a **small** set of data, i.e. data-parallel processing (having many programs open at once). 

A GPU is good at doing **simple manipulations** on a **large** set of data, i.e. data-parallel computing. It used to be mostly good for graphic operations (matrix operations = simple manips on a large dataset, but more and more computations is becoming possible on GPU alone. It's more efficient because it has less instruction decoding overhead.    

Note that they both enable SIMD (Single Instruction, Multiple Data): the CPU parallelize instructions, and the GPU parallelize pipelines.  

How do the CPU and the GPU relate to each other?   
* The CPU orchestrates the GPU's work  
* A GPU is a special kind of CPU
* New systems have GPU integrated in the CPU  

How do apps use the CPU and GPU?   
Usually, applications run on the CPU and GPU using mechanisms provided by the Operating System.  

How do we measure their power?   
In Hz = CPU clock speed = how much work a processor can do in a certain time. 1GHz = 1 billion bits per second.  
Number of cores = how many bits can be processed at once.
Example:  
MacBook pro CPU = 3.8GHz. Dual core 2.2 GHz can process 4.4 billion bits per second.   

What's one pitfall of a GPU?   
Because large blocks are used, there are more parallel processing units, so a single GPU instruction uses more transistors => more space and energy needed, more heat is generated.   

How does it look inside?  
E.g. cores.  
See Alex Danilo on threads. TBD.  

Sources:
https://superuser.com/questions/308771/why-are-we-still-using-cpus-instead-of-gpus
https://developers.google.com/web/updates/2018/09/inside-browser-part1  
https://stackoverflow.com/questions/27333815/cpu-simd-vs-gpu-simd

## RAM

The RAM is a temporary storage area from which retrieval is faster than from disk / permanent storage.
When the CPU needs to process some data, the data will be first loaded onto the RAM so that the CPU can retrieve it faster, which will speed things up alltogether. CPU is the brain, RAM is the book, permanent storage is the bookshelf.
NB: GPU also uses RAM, new systems have GPU integrated in the CPU.
Source: https://superuser.com/questions/78362/what-is-the-relationship-between-cpu-usage-and-ram

## Processes and threads

A process is an application’s executing program.  
A thread lives inside of process and executes any part of its process's program.

### When you start an application 
- A process is created.
- The program might create thread(s) to help it do work
- The OS gives the process a "slab" of memory to work with and all application state is kept in that private memory space.

### At runtime: 
A process can ask the OS to spin up another process to run different tasks. When this happens, different parts of the memory are allocated for the new process. If two processes need to talk, they can do so by using Inter Process Communication (IPC). Many applications are designed to work this way so that if a worker process get unresponsive, it can be restarted without stopping other processes which are running different parts of the application.

### When you close the application
- the process goes away
- the OS frees up the memory.  


<p align="center">
<img width="400" src="https://developers.google.com/web/updates/images/inside-browser/part1/workerprocess.svg">   
  	<div align="center"><sub><sup>Src: @kosamari on https://developers.google.com/web/updates/2018/09/inside-browser-part1</sup></sub></div> 
</p>  
