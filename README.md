# How Computers Work (Part 1): Hardware

## CC Statement

## Overview/Goals

## Acknowledgements

# ToC

# Lecture/Live Coding

# Overview

LAPTOP SPEC COMPARISON IMAGE

<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

If you've ever purchased a laptop, you may have encountered an overwhelming number of details about different aspects of the product. This information is often referred to as "specifications" (or "specs"). The next few labs will focus on breaking down some of these components to better understand the hardware and software building blocks that make up a computer.

Specifically, we'll be using a framework called the `von Neumann architecture`, named for the Hungarian-American scientist [John von Neumann](https://en.wikipedia.org/wiki/John_von_Neumann). Developed in the 1940s, this computer design framework is based on the principle that data and instructions have the same logical significance to the computer. Rather than separate data and instructions, the von Neumann architecture conceptualizes a computer system that is able to store instructions and data. This is referred to as a `stored-program computer`.

To learn more about von Neumann architecture:
- [Wikipedia](https://en.wikipedia.org/wiki/Von_Neumann_architecture)
- John von Neumann, "[First Draft of a Report on the EDVAC](http://web.mit.edu/STS.035/www/PDFs/edvac.pdf)", *IEEE Annals of the History of Computing* 15:4 (1993): 29-43. Originally published in 1945.

VON NEUMANN IMAGE

<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

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
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=517ac0ae-6466-4508-9264-aef401054b25">ALU & Memory</a></td>
  </tr>
  </table>

## Key Terms

ALU DIAGRAM
<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

**Arithmetic Logic Unit**
- "An arithmetic logic unit (ALU) is a combinational digital electronic circuit that performs arithmetic and bitwise operations on integer binary numbers" ([Wikipedia](https://en.wikipedia.org/wiki/Arithmetic_logic_unit))

REGISTER DIAGRAM
<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

**Memory**
- "In computing, memory refers to a device that is used to store information for immediate use in a computer or related computer hardware device" ([Wikipedia](https://en.wikipedia.org/wiki/Computer_memory))

**Registers**
- "In computer architecture, a processor register is a quickly accessible location available to a computer's central processing unit (CPU). Registers usually consist of a small amount of fast storage" ([Wikpedia](https://en.wikipedia.org/wiki/Processor_register))

**Random Access Memory (RAM)**
- "Random-access memory (RAM) is a form of computer memory that can be read and changed in any order, typically used to store working data and machine code" ([Wikipedia](https://en.wikipedia.org/wiki/Random-access_memory))
- RAM is controlled by the CPU and can include data and instructions

**Persistant Memory**
- Physical storage (magnetic disks, solid state disks, magnetic tape, etc) that retains information even when the device is powered off

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLScQoRbyDYB2Cisg_AmfMhUqj8qXn0ZbeuembRhQpOnbb64I2g/viewform?usp=sf_link">ALU & Memory Comprehension Check</a></td>
  </tr>
  </table>

COMPREHENSION CHECK

Describe core components of the ALU

RAM vs persistant memory

## Application

DATA PATH SIMULATOR

# CPU & the Fetch-Execute Cycle

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=517ac0ae-6466-4508-9264-aef401054b25">CPU & the Fetch-Execute Cycle</a></td>
  </tr>
  </table>

## Key Terms

**Input and Output (I/O)**
- I/O devices provide inputs to the system and enable the computer to provide output
- Input device examples: keyboard, mouse, network card, etc.
- Output device examples: monitor, display, printer, etc.

CPU DIAGRAM
<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

**Processor (or processing unit)**
- "In computing, a processor or processing unit is an electronic circuit which performs operations on some external data source, usually memory or some other data stream. The term is frequently used to refer to the central processor (central processing unit)" ([Wikipedia](https://en.wikipedia.org/wiki/Processor_(computing)))

**CPU**
- "A central processing unit (CPU), also called a central processor or main processor, is the electronic circuitry within a computer that executes instructions that make up a computer program. The CPU performs basic arithmetic, logic, controlling, and input/output (I/O) operations specified by the instructions…Principal components of a CPU include the arithmetic logic unit (ALU) that performs arithmetic and logic operations, processor registers that supply operands to the ALU and store the results of ALU operations, and a control unit that orchestrates the fetching (from memory) and execution of instructions by directing the coordinated operations of the ALU, registers and other components" ([Wikipedia](https://en.wikipedia.org/wiki/Central_processing_unit))

**Bus**
- "In computer architecture, a bus…is a communication system that transfers data between components inside a computer, or between computers. This expression covers all related hardware components (wire, optical fiber, etc.) and software" ([Wikipedia](https://en.wikipedia.org/wiki/Bus_(computing)))

**Instruction Register (IR)**
- Register with the instruction that is currently being executed

FETCH-EXECUTE CYCLE DIAGRAM
<p align="center"><img src="https://github.com/kwaldenphd/bits-bytes/blob/main/images/Image_2.png?raw=true" width="500"></p>

**Fetch-Execute Cycle**
- Computer processing cycle that includes four main steps:
  * Fetch instruction
  * Decode instruction
  * Get data (if needed)
  * Execute instruction

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLScQoRbyDYB2Cisg_AmfMhUqj8qXn0ZbeuembRhQpOnbb64I2g/viewform?usp=sf_link">CPU & Fetch-Execute Comprehension Check</a></td>
  </tr>
  </table>

COMPREHENSION CHECK

Which of following is NOT a core component of the CPU

What are the core components of the CPU

Fetch execute cycle- what isn't part of that

## Application

SECOND SIMULATOR WITH MAIN MEMORY


# Assembly Language




## Key Terms

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLScQoRbyDYB2Cisg_AmfMhUqj8qXn0ZbeuembRhQpOnbb64I2g/viewform?usp=sf_link">Assembly Language Comprehension Check</a></td>
  </tr>
  </table>


## Application

THIRD SIMULATOR


# Putting It All Together

Windows 11 processor requirements

https://blogs.windows.com/windows-insider/2021/08/27/update-on-windows-11-minimum-system-requirements-and-the-pc-health-check-app/

https://www.cnet.com/tech/services-and-software/microsofts-strict-windows-11-device-requirements-have-one-exception-what-to-know/

## Final Questions

QX: Back to original laptop specs. What do you understand better/more deeply

QX: What are specs for your own computer, what do they mean

Mac: https://support.apple.com/guide/system-information/get-system-information-syspr35536/mac
PC: https://www.lifewire.com/how-to-get-your-computer-specs-3506998
