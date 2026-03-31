# Chapter 1

## 1. Information Is Bits

Programs begin as a *source file* that a programmer creates with an editor and saves in a text file. It is a sequence of bits, each with a value of 0 or 1, organized in 8-bit chunks called bytes. Each byte represents some text character in the program.

> **Origins of the C programming language**
>
> C was developed by Dennis Ritchie of Bell Labs from 1969 to 1973. Kernighan and Ritchie describe ANSI C in the classic book known as [K&R]().

## 2. Programs Are Translated by Other Programs into Different Forms

A program begins life as a high-level C program since it is in human readable form. In order to run the program on the system, the individual statements must be translated by other programs into a sequesnce of low-level machine-code instructions. These instructions are packaged in a form called an executable object program stored as a binary disk file.

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
2. **Compilation phase** - The compiler (cc1) translates the text file into an assembly file with suffix `.s`. Each line is a defenition of one low-level machine-language instruction in a textual form.
3. **Assembly phase** - The assembler (as) translates the assembly file into machine-language instructions and packages them in a form known as a *relocatable object program*, and stores the result in a file with the `.o` suffix.
4. **Linking phase** - The linker (ld) handles the merging of the program with other files in the standard C library. It results in an executable file that is ready to be loaded into memory and executed by the system.

> **The GNU project**
>
> The GNU project is a tax-exempt charity started by Richard Stallman in 1984, with the goal of developing a complete Unix-like system whose source code is unencumbered by restrictions on how it can be modified or distributed. The GNU project has developed an environment with all the major components of a Unix operating system, except for the kernel, which was developed separately by the Linux project.

## 3. It Pays to Understand How Compilation Systems Work

## 4. Processors Read and Interpret Instructions Stored in Memory

## 5. Caches Matter

## 6. Storage Devices Form a Hierarchy

## 7. The Operating System Manages the Hardware

## 8. Systems Communicate with Other Systems Using Networks

## 9. Important Themes
