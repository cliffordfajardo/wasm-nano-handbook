## CPU vs GPU

CPU = central processing unit.

A CPU is good at doing complex manipulations on a small set of data.  
A GPU is good at doing simple manipulations on a large set of data.

MacBook pro CPU = 3.8GHz (= CPU clock speed = how much work a processor can do in a certain time. 1GHz = 1 billion bits per second, and # of cores = how many bits can be processed at once. Dual core 2.2 GHz can process 4.4 billion bits per second).

How a GPU works: it's a special kind of CPU, designed to perform SIMD = Single Instruction, Multiple Data. It's more efficient because less instruction-decoding overhead. But because large blocks are used, there are more parallel processing units, so a single GPU instructions uses more transistors (=> more space and energy needed, more heat is generated).

Only the GPU is very good at data-parallel computing. It used to be only good for graphic operations, but more and more computations is becoming possible on GPU alone.

CPU is good at parallel processing, i.e. having many programs open at once.

When you start an application on your computer or phone, the CPU and GPU are the ones powering the application. Usually, applications run on the CPU and GPU using mechanisms provided by the Operating System.

Source:
https://superuser.com/questions/308771/why-are-we-still-using-cpus-instead-of-gpus
https://developers.google.com/web/updates/2018/09/inside-browser-part1

## CPU, GPU and RAM

The RAM is a temporary storage area from which retrieval is faster than from disk / permanent storage.
When the CPU needs to process some data, the data will be first loaded onto the RAM so that the CPU can retrieve it faster, which will speed things up alltogether. CPU is the brain, RAM is the book, permanent storage is the bookshelf.
NB: GPU also uses RAM, new systems have GPU integrated in the CPU.
Source: https://superuser.com/questions/78362/what-is-the-relationship-between-cpu-usage-and-ram

## The stack and the heap

TBD

## Processes and threads

A process is an application’s executing program.
A thread is the one that lives inside of process and executes any part of its process's program.

When you start an application:

- A process is created.
- The program might create thread(s) to help it do work
- The OS gives the process a "slab" of memory to work with and all application state is kept in that private memory space.

At runtime:
A process can ask the OS to spin up another process to run different tasks. When this happens, different parts of the memory are allocated for the new process. If two processes need to talk, they can do so by using Inter Process Communication (IPC). Many applications are designed to work this way so that if a worker process get unresponsive, it can be restarted without stopping other processes which are running different parts of the application.

When you close the application:

- the process goes away
- the OS frees up the memory.

One illustration: https://developers.google.com/web/updates/images/inside-browser/part1/workerprocess.svg

https://developers.google.com/web/updates/2018/09/inside-browser-part1
