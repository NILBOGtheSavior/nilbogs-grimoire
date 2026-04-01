# Chapter 1

## 1. Information Is Bits

Programs begin as a *source file* that a programmer creates with an editor and saves in a text file. It is a sequence of bits, each with a value of 0 or 1, organized in 8-bit chunks called bytes. Each byte represents some text character in the program.

> **Origins of the C programming language**
>
> C was developed by Dennis Ritchie of Bell Labs from 1969 to 1973. Kernighan and Ritchie describe ANSI C in the classic book known as [K&R]().

## 2. Programs Are Translated by Other Programs into Different Forms

A program begins life as a high-level C program since it is in human-readable form. In order to run the program on the system, the individual statements must be translated by other programs into a sequence of low-level machine-code instructions. These instructions are packaged in a form called an executable object program stored as a binary disk file.

```
          ┌───────────┐          ┌───────────┐          ┌───────────┐          ┌───────────┐
  app.c   │    Pre-   │  app.i   │ Compiler  │  app.s   │ Assembler │  app.o   │   Linker  │ hello
─────────>│ Processor │─────────>│   (cc1)   │─────────>│   (as)    │─────────>│    (ld)   │─────────>
 Source   │   (cpp)   │ Modified │           │ Assembly │           │ Relocatable          │ Executable
 program  └───────────┘ source   └───────────┘ program  └───────────┘ object   └───────────┘ object
 (text)                 program                (text)                 programs               (binary)
                        (text)                                        (binary)
```

These programs are known collectively as the compilation system.

1. **Preprocessing phase** - The original C program is modified according to the directives that begin with the `#` character. This results in another C program with the `.i` suffix.
2. **Compilation phase** - The compiler (cc1) translates the text file into an assembly file with suffix `.s`. Each line is a definition of one low-level machine-language instruction in a textual form.
3. **Assembly phase** - The assembler (as) translates the assembly file into machine-language instructions and packages them in a form known as a *relocatable object program*, and stores the result in a file with the `.o` suffix.
4. **Linking phase** - The linker (ld) handles the merging of the program with other files in the standard C library. It results in an executable file that is ready to be loaded into memory and executed by the system.

> **The GNU project**
>
> The GNU project is a tax-exempt charity started by Richard Stallman in 1984, with the goal of developing a complete Unix-like system whose source code is unencumbered by restrictions on how it can be modified or distributed. The GNU project has developed an environment with all the major components of a Unix operating system, except for the kernel, which was developed separately by the Linux project.

## 3. It Pays to Understand How Compilation Systems Work

There are important reasons why programmers need to understand how compilation systems work:

- **Optimizing program performance** - In order to make good coding decisions in our C programs, we need a basic understanding of machine-code and how the compiler translates different C statements into this code.
- **Understanding link-time errors** - The most perplexing errors are related to the operation of the linker, especially for large software systems. Understanding this helps with debugging.
- **Avoiding security holes** - For years, buffer overflow vulnerabilities have accounted for many of the security holes in network and internet servers.

## 4. Processors Read and Interpret Instructions Stored in Memory

### Hardware organization of a typical system

**Buses**

Buses are electrical conduits that carry bytes of information back and forth between components. They are designed to transfer fixed-size chunks of bytes known as words. The number of bytes in a word is a fundamental system parameter that varies across systems. Most machines today have word sizes of 4 or 8 bytes.

**I/O Devices**

Input/output (I/O) devices are the connection to the external world. Each I/O device is connected to the I/O bus by either a controller or an adapter. Controllers are chip sets in the device itself or on the motherboard. An adapter is a card that plugs into a slot on the motherboard.

**Main Memory**

Memory is a temporary storage device that holds the program and the data it executes. Memory consists of a collection of dynamic random access memory (DRAM) chips, organized as a linear array of bytes, each with its own unique address starting at zero.

**Processor**

The central processing unit (CPU) is the engine that interprets instructions stored in main memory. At its core is a word-size storage device (register) called the program counter (PC). At any time, the PC points at some machine-language instruction in main memory.

There are only a few operations that the processor can execute. They revolve around main memory, the register file, and the arithmetic/logic unit (ALU).

### Running a program

Initially, the shell is executing its instructions, waiting for a command. As we type characters, the shell program reads each one into a register and then stores it in memory. When we hit enter, the shell knows that we have finished typing the command. The shell loads the executable by executing a series of instructions that copies the code and data from the program object file from the disk into main memory.

Using a technique known as direct memory access (DMA), the data travels directly from disk to main memory without passing the processor. The processor then begins executing the machine-language in the programs `main` routine.

## 5. Caches Matter

The system spends a lot of time moving information from one place to another. The machine instructions in a program are originally stored on the disk. When a program is loaded, they are copied from main memory into the processor. This copying is considered overhead that slows down the "real work" of the program, thus, a major goal for system designers is to make these copy operations run as fast as possible.

Larger storage devices are slower than smaller storage devices, and faster devices are more expensive to build that their slower counterparts.

A typical register file stores a few hundred bytes of information, as opposed to billions of bytes in the main memory. However, the processor can read data from the register file almost 100 times faster than from memory.

As semiconductor technology progresses, the processor-memory gap continues to increase, as it is easier and cheaper to make processors run faster than it is to make main memory run faster. To deal with processor-memory gaps, faster storage devices called chache memories that serve as temporary stagin areas for information that the processor is likely to need in the near future.

- L1 cache holds tens of thousands of bytes.
- L2 cache holds hundreds of thousands to millions of bytes, but takes 5 times longer to access than L1 cache.
- L3 cache is in newer system.

By setting up caches to hold data that are likely to be accessed often, we can perform most memory operations using the fast caches.

## 6. Storage Devices Form a Hierarchy

The register file occupies the top level in the hierarchy, which is known as level 0 (L0). The main idea of a memory hierarchy is that storage at one level serves as cache for storage at the next lower level.

## 7. The Operating System Manages the Hardware

The operating system is the layer of software interposed between the application program and hardware. All attempts by an application to manipulate the hardware must go through the operating system.

```
 ┌───────────────────────────────────────────┐
 │            Application programs           │
 ├───────────────────────────────────────────┤} Software
 │              Operating system             │
 ├─────────────┬───────────────┬─────────────┤
 │  Processor  │  Main Memory  │ I/O devices │} Hardware
 └─────────────┴───────────────┴─────────────┘
```

```
                   Processes
 ┌─────────────────────┴─────────────────────┐
 |                      Virtual memory       |
 |             ┌───────────────┴─────────────┐
 |             |                    Files    |
 |             |               ┌──────┴──────┐
 ┌─────────────┬───────────────┬─────────────┐
 │  Processor  │  Main Memory  │ I/O devices │
 └─────────────┴───────────────┴─────────────┘
```

The operating system has two primary pusposes: to protext the hardware from misuse by runaway applications and to provice applications with simple and uniform mechanisms for manipulating complicated and different low-level hardware devices.

When we run a program, it appears to have exclusive use of both the processor, main memory, and I/O devices. The processor appears to execute the instructions in the program one after the other, without interruption, and the code and data of the program appear to be the only objects in the system's memory.

### Processes

A process is the OS's abstraction for running a program. Multiple processes can run concurrently on the same system, and each process appears to have exclusive use of the hardware. Traditional systems could only execute one program at a time, while newer multi-core processors can execute several programs simultaneously. A single CPU can appear to execute multiple processes concurrently by having the processor switch among them. This mechanism is known as *context switching*.

The OS keeps track of all state information that the process needs in order to run. This state, which is known as the *context*, includes information such as the curent values of the PC, the register file, and the contents of main memory. When the OS decides to transfer control from the current process to some new process, it performs a context switch by saving the context of the current process, restoring the context of the new process, and then passing control to the new process.

The transition from one process to another is managed my the OS kernel. The kernel is the portion of the OS code that is always resident in memory. When an application program requires some action by the OS, it executes a special *system call* instruction, transferring control to the kernel. The kernel then performs the requested operation and returns back to the application program.

> **Note**
>
> The kernel is not a separate process, but a collection of code and data structures that the system uses to manage all processes.

### Threads

In modern systems, a process can consist of multiple execution units called threads, each running in the context of the process and sharing the same code and global data.

### Virtual memory

*Virtual memory* is an abstraction that provides each process with the illusion that it has exclusive use of main memoty. Each process has the same uniform view of memory, which is known as its virtual address space. In Linux, the topmost region of the address space is reserved for code and data in the operating system that is common to all processes. The lower region of the address space holds the code and data defined by the user's process.

- **Program code and data** - Code begins at the same fixed address for all processes, followed by data locations that correspond to global C variables.. The code and data areas are initialized directly from the conents of an executable object file.
- **Heap** - The code and data areas are followed immediately by the run-time heap. The heap expands and contracts dynamically at run-time as a result of calls to C standard library routines such as `malloc` and `free`.
- **Shared libraries** - Near the middle of the address space is an area that holds the code and data for shared libraries such as the C standard library and the math library.
- **Stack** - At the top of the user's virtual address space is the user stack that the compiler uses to implement function calls. The user stack expands and contracts dynamically suring the execution of the program.
- **Kernel virual memory** - The top region of the address space is reserved for the kernel. Application programs are not allowed to read or write the contents of this area or to directly call functions defined in kernel code. Instead, they must invoke the kernel to perfrom these operations.

### Files

A *file* is a sequence of bytes. Every I/O device, including disks, keyboards, displays, and networks is modeled as a file. All I/O in the system is perfromed by reading and writing files, using a subset of system calls known as *Unix I/O*.

## 8. Systems Communicate with Other Systems Using Networks

From the point of view of the system, a network can be viewed as just another I/O device.

Copying information from one machine to another has become one of the most important uses of computer systems. For example, email, instant messaging, the World Wide Web, FTP, and telnet are all based on the ability to copy information over a network.

The exchange of information between clients and server is typical of all network applications.
