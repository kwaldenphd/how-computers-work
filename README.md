# How Computers Work (Part 1): Hardware

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview and Goals

This lab covers a variety of topics related to how computers "work." This lab is designed to help you gain an understanding of how the basic logical and mathematical operations underlying computation are performed mechanically. We will also use a simulation of CPU architecture to learn more about how an instruction is processed along the CPU data path cycle and how values from memory are incorporated into CPU instructions. We are doing this to gain more experience with understanding a computer’s mechanical operations at a higher level of abstraction. Finally, this lab covers reading and writing basic assembly language, to help us see the 0s and 1s underneath higher level programming and apply them to basic algorithms.

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=72439895-e9e2-47bc-b8b2-aef4014d339f">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements

The author consulted Chapter 5, "Computing Components" from Nell Dale and John Lewis' *[Computer Science Illuminated, Seventh Edition](https://www.jblearning.com/catalog/productdetails/9781284155617)* textbook (Jones & Barlett Learning, 2020; ISBN: 9781284155617) when writing this lab.

Sections of this lab are based on the "Data path & memory" lab:
- Created: Jerod Weinman, 16 March 2009
- Modified: Jerod Weinman, 20 April 2011
- Modified: Jerod Weinman, 4 April 2014
- Portions adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.1-14.6.

Sections of this lab are based on the "Machine language" lab:
- Created: Jerod Weinman, March 16, 2009
- Revised: Janet Davis, April 27, 2012
- Revised: Janet Davis, March 12, 2013
- Revised: Jerod Weinman, 4 April 2014
- Adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.9, 14.10, and 14.13. 

This lab's lecture segments were adapted from the following PBS *[Crash Course Computer Science](https://www.pbs.org/show/crash-course-computer-science/)* episodes:
- "[How Computers Calculate - the ALU](https://www.pbs.org/video/how-computers-calculate-the-alu-crash-course-computer-sci-sm5zov/)"
- "[Registers & RAM](https://www.pbs.org/video/registers-and-ram-crash-course-computer-science-6-lddkcd/)"
- "[The Central Processing Unit (CPU)](https://www.pbs.org/video/the-central-processing-unit-cpu-crash-course-computer-sci-v5aynn/)"
- "[Instructions & Programs](https://www.pbs.org/video/instructions-programs-crash-course-computer-science-8-ai4emg/)"

# Table of Contents
- [Lecture & Live Coding](#lecture--live-coding)
- [Key Concepts](#key-concepts)
- [Lab Notebook Template](#lab-notebook-template)
- [Von Neumann Architecture](#von-neumann-architecture)
- [ALU & Memory](#alu--memory)
- [CPU & the Fetch-Execute Cycle](#cpu--the-fetch-execute-cycle)
- [Assembly Language](#assembly-language)
- [Putting It All Together](#putting-it-all-together)
- [Lab Notebook Questions](#lab-notebook-questions)

## Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:
 
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=72439895-e9e2-47bc-b8b2-aef4014d339f">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Key Concepts

[Click here](https://github.com/kwaldenphd/how-computers-work/blob/main/key-concepts.md) for a full list of key concepts and definitions for this lab.

## Lab Notebook Template

[Link to lab notebook template](https://docs.google.com/document/d/1SpHmyZkN7b5wmtY0n8y5jI6JxBanZXg8UVZOoNPIv_o/copy) (ND users, Google Doc)

# Von Neumann Architecture

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Laptop_Spec_Comparison.png?raw=true" width="750"></p>

If you've ever purchased a laptop, you may have encountered an overwhelming number of details about different aspects of the product. This information is often referred to as "specifications" (or "specs"). The next few labs will focus on breaking down some of these components to better understand the hardware and software building blocks that make up a computer.

Specifically, we'll be using a framework called the `von Neumann architecture`, named for the Hungarian-American scientist [John von Neumann](https://en.wikipedia.org/wiki/John_von_Neumann). Developed in the 1940s, this computer design framework is based on the principle that data and instructions have the same logical significance to the computer. Rather than separate data and instructions, the von Neumann architecture conceptualizes a computer system that is able to store instructions and data. This is referred to as a `stored-program computer`.

To learn more about von Neumann architecture:
- [Wikipedia](https://en.wikipedia.org/wiki/Von_Neumann_architecture)
- John von Neumann, "[First Draft of a Report on the EDVAC](http://web.mit.edu/STS.035/www/PDFs/edvac.pdf)", *IEEE Annals of the History of Computing* 15:4 (1993): 29-43. Originally published in 1945.

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Von_Neumann_Architecture.png?raw=true" width="500"></p>

The core components of the von Neumann architecture:
- Input and output
- Control unit
- Arithmetic and logic unit (ALU)
- Memory unit
  * The last three components (control unit, ALU, memory) make up the central processing unit (CPU) 

# ALU & Memory

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b3c6700d-f527-4cc6-b4aa-aef40109af8e">ALU & Memory</a></td>
  </tr>
  </table>

## Key Concepts

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/ALU_Diagram.gif?raw=true" width="500"></p>

**Arithmetic Logic Unit**
- "An arithmetic logic unit (ALU) is a combinational digital electronic circuit that performs arithmetic and bitwise operations on integer binary numbers" ([Wikipedia](https://en.wikipedia.org/wiki/Arithmetic_logic_unit))

**Memory**
- "In computing, memory refers to a device that is used to store information for immediate use in a computer or related computer hardware device" ([Wikipedia](https://en.wikipedia.org/wiki/Computer_memory))

**Registers**
- "In computer architecture, a processor register is a quickly accessible location available to a computer's central processing unit (CPU). Registers usually consist of a small amount of fast storage" ([Wikpedia](https://en.wikipedia.org/wiki/Processor_register))

**Random Access Memory (RAM)**
- "Random-access memory (RAM) is a form of computer memory that can be read and changed in any order, typically used to store working data and machine code" ([Wikipedia](https://en.wikipedia.org/wiki/Random-access_memory))
- RAM is controlled by the CPU and can include data and instructions

**Persistent Memory**
- Physical storage (magnetic disks, solid state disks, magnetic tape, etc) that retains information even when the device is powered off

[Click here](https://github.com/kwaldenphd/how-computers-work/blob/main/key-concepts.md) for a full list of key concepts and definitions for this lab.

## Comprehension Check

<table>
 <tr><td>
<img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/clipboard.png?raw=true" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSeQMbwN4rnIyAkuVVkGGOK2hQdvH1X6gzsjXO1ZvQi1pRJHnw/viewform?usp=sf_link">ALU & Memory Comprehension Check</a></td>
  </tr>
  </table>

## Application

Q1: What types of inputs does the ALU accept? Or, what kind of data can be passed to the ALU?

Q2: What are some of the differences between RAM and persistent memory?

# CPU & the Fetch-Execute Cycle

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=023c10d6-1764-48bf-a75d-aef40109b030">CPU & the Fetch-Execute Cycle</a></td>
  </tr>
  </table>

## Key Concepts

**Input and Output (I/O)**
- I/O devices provide inputs to the system and enable the computer to provide output
- Input device examples: keyboard, mouse, network card, etc.
- Output device examples: monitor, display, printer, etc.

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Von_Neumann_Flow.png?raw=true" width="500"></p>

**Processor (or processing unit)**
- "In computing, a processor or processing unit is an electronic circuit which performs operations on some external data source, usually memory or some other data stream. The term is frequently used to refer to the central processor (central processing unit)" ([Wikipedia](https://en.wikipedia.org/wiki/Processor_(computing)))

**CPU**
- "A central processing unit (CPU), also called a central processor or main processor, is the electronic circuitry within a computer that executes instructions that make up a computer program. The CPU performs basic arithmetic, logic, controlling, and input/output (I/O) operations specified by the instructions…Principal components of a CPU include the arithmetic logic unit (ALU) that performs arithmetic and logic operations, processor registers that supply operands to the ALU and store the results of ALU operations, and a control unit that orchestrates the fetching (from memory) and execution of instructions by directing the coordinated operations of the ALU, registers and other components" ([Wikipedia](https://en.wikipedia.org/wiki/Central_processing_unit))

**Bus**
- "In computer architecture, a bus…is a communication system that transfers data between components inside a computer, or between computers. This expression covers all related hardware components (wire, optical fiber, etc.) and software" ([Wikipedia](https://en.wikipedia.org/wiki/Bus_(computing)))

**Instruction Register (IR)**
- Register with the instruction that is currently being executed

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fetch_Execute_Cycle.png?raw=true" width="500"></p>

**Fetch-Execute Cycle**
- Computer processing cycle that includes four main steps:
  * Fetch instruction
  * Decode instruction
  * Get data (if needed)
  * Execute instruction

[Click here](https://github.com/kwaldenphd/how-computers-work/blob/main/key-concepts.md) for a full list of key concepts and definitions for this lab.

## Comprehension Check

<table>
 <tr><td>
<img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/clipboard.png?raw=true" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSffdR1H3vNmMPIjRKvhaS1DkzysyDJ1h9vFjHDW_CGP_qmh5g/viewform?usp=sf_link">CPU & Fetch-Execute Comprehension Check</a></td>
  </tr>
  </table>

## Application

Q3: Describe the three main steps of the fetch-execute cycle in your own words.

# Assembly Language

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=bae0c40a-1e2d-43bc-b27c-aef40109b060">Assembly Language</a></td>
  </tr>
  </table>

## Key Concepts

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Pep9_Instruction_Format.png?raw=true" width="500"></p>

**Assembly Language**
- "In computer programming, assembly language...is any low-level programming language with a very strong correspondence between the instructions in the language and the architecture's machine code instructions. Assembly language usually has one statement per machine instruction (1:1)...Because each assembly depends on the machine code instructions, each assembly language is specific to a paticular computer architecture" ([Wikipedia](https://en.wikipedia.org/wiki/Assembly_language))

**Assembler**
- "An assembler program creates object code by translating combinations of mnemonics and syntax for operations and addressing modes into their numerical equivalents. This representation typically includes an operation code ('opcode') as well as other control bits and data. The assembler also calculates constant expressions and resolves symbolic names for memory locations and other entities" ([Wikipedia](https://en.wikipedia.org/wiki/Assembly_language#Assembler))

**Instruction Specifier**
- Typically the first byte of an instruction. If present, it indicates which operation is being performed. Also tells the computer how to process the operand.

**Operand Specifier**
- Typically the second and third bytes in an instruction. If present, it can hold the operand or its address (location).

**Operation Codes (opcodes)**
- Typically 4-8 bits. It indicates the instruction specifier format and can include a register specifier.

**Addressing Mode**
- Typically 3 bits. It indicates how to interpret the operand specifier.

[Click here](https://github.com/kwaldenphd/how-computers-work/blob/main/key-concepts.md) for a full list of key concepts and definitions for this lab.

## Comprehension Check

<table>
 <tr><td>
<img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/clipboard.png?raw=true" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSc1CvbF9ttUsh6vQhy3dlCIG3peps0y1jIlbgi7IrIPXIEe-A/viewform?usp=sf_link">Assembly Language Comprehension Check</a></td>
  </tr>
  </table>

## Application

Q4: Describe the relationship of assembly language and machine language (or machine code) in your own words.

# Putting It All Together

"All computers have a CPU that can be divided into two pieces. The first is the datapath, which is a network of storage units (registers) and arithmetic and logic units...connected by buses...where the timing is controlled by clocks." (Linda Null and Julia Lobur, 2006. *[The Essentials of Computer Organization and Architecture](https://www.oreilly.com/library/view/the-essentials-of/9781284033144/)*, pp. 2016.)

Let's go back to the laptop specs we looked at in the beginning of this lab.

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Laptop_Spec_Comparison.png?raw=true" width="750"></p>

Hopefully we're gaining familiarity with some of these terms and concepts.

Let's find the hardware specs for your personal computer (or a school computer you can access):
- [Mac users](https://support.apple.com/guide/system-information/get-system-information-syspr35536/mac)
- [PC users](https://www.lifewire.com/how-to-get-your-computer-specs-3506998)
- [Chromebook](https://www.lifewire.com/how-to-check-chromebook-specs-hardware-4782658)
- [Linux](https://www.makeuseof.com/check-system-details-and-hardware-information-on-linux/)

<blockquote>Q5: How would you describe some of these specifications in your own words, using terms and concepts covered in this lab? Specific aspects of your computer's system to discuss: persistent memory, short-term memory (RAM), processor, graphics, ports or peripherals</blockquote>

You may be wondering if these specifications matter for your regular computer use. That's a fair question. 

Your computer's input devices control what types of devices you can connect to the computer, from the number and type of USB ports to HDMI connections and other adapters.

Your computer's output devices, especially the display, control screen size, resolution, and other aspects of the visual interface.

Sometimes, operating system updates can run into compatibility issues with the underlying computer hardware. For example, the hardware in Professor Walden's second-generation iPad stopped supporting iOS updates in 2016, meaning the tablet isn't able to run current versions of most apps or programs. Mac operating system updates often have specific hardware requirements and [can only be rolled out on select models](https://support.apple.com/en-us/HT212551). The recent Windows 11 roll out has very specific minimum system requirements.

Learn more about the Windows 11 rollout:
- [Windows](https://blogs.windows.com/windows-insider/2021/08/27/update-on-windows-11-minimum-system-requirements-and-the-pc-health-check-app)
- [CNet](https://www.cnet.com/tech/services-and-software/microsofts-strict-windows-11-device-requirements-have-one-exception-what-to-know)

# Lab Notebook Questions

[Link to lab notebook template](https://docs.google.com/document/d/1SpHmyZkN7b5wmtY0n8y5jI6JxBanZXg8UVZOoNPIv_o/copy) (ND users, Google Doc)

Q1: What types of inputs does the ALU accept? Or, what kind of data can be passed to the ALU?

Q2: What are some of the differences between RAM and persistent memory?

Q3: Describe the three main steps of the fetch-execute cycle in your own words.

Q4: Describe the relationship of assembly language and machine language (or machine code) in your own words.

Q5: Find the hardware specs for your personal computer (or a school computer you can access). How would you describe some of these specifications in your own words, using terms and concepts covered in this lab?
- [Mac users](https://support.apple.com/guide/system-information/get-system-information-syspr35536/mac)
- [PC users](https://www.lifewire.com/how-to-get-your-computer-specs-3506998)
- [Chromebook](https://www.lifewire.com/how-to-check-chromebook-specs-hardware-4782658)
- [Linux](https://www.makeuseof.com/check-system-details-and-hardware-information-on-linux/)
