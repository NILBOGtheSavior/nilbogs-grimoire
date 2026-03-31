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

## 7. The Operating System Manages the Hardware

## 8. Systems Communicate with Other Systems Using Networks

## 9. Important Themes
