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

## Lab Notebook Template

[Link to lab notebook template](https://docs.google.com/document/d/1SpHmyZkN7b5wmtY0n8y5jI6JxBanZXg8UVZOoNPIv_o/copy) (ND users, Google Doc)
- Simulator screenshots are HIGHLY recommended.
  * Windows ([Snipping Tool](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b) for folks running older versions of Windows; [Snip & Sketch](https://www.lifewire.com/snip-and-sketch-windows-10-4774799) for folks running updated versions)
  * [Mac](https://support.apple.com/en-us/HT201361)
  * [Google Chromebook](https://support.google.com/chromebook/answer/10474268?hl=en)
- [Tutorial for adding images/tables/drawings to a Google Doc](https://www.techrepublic.com/article/how-to-add-images-tables-and-drawings-to-a-google-doc-file/)

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
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=517ac0ae-6466-4508-9264-aef401054b25">ALU & Memory</a></td>
  </tr>
  </table>

## Key Terms

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

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_1.png?raw=true" width="500"></p>

Open the [Knob & Switch Datapath 1 Simulator](http://www.dave-reed.com/book/Chapter14/datapath/datapath.html) in a new browser window. This simple CPU contains four registers, but no control unit. You will be the control unit that directs which registers are operated on and which operations are done.

Take a look at the top box that says `Register Bank.` At the right are two command knobs, `A Bus Address` and `B Bus Address.` These knobs specify which registers should be read as inputs to the ALU. You can click on each knob to turn it.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_2.png?raw=true" width="500"></p>

Set the `A bus` address to `R2` and the `B bus` address to `R1`. 

<blockquote>Q1: Based on these bus settings, what values do you expect to show along the A and B bus?</blockquote>

The register values are the textboxes with a green background. Currently, all the register default values are zero.  

Set the value of `R1` to 42. Set the value of `R2` to 31. Check that `Animation Speed` is set on `Medium` and `Number Base` is set to `+-10.`

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_2.png?raw=true" width="500"></p>

<blockquote>Q2: What happens when you click <code>Execute</code>? Are the <code>A bus</code> and <code>B bus</code> values what you expected? Why or why not?</blockquote>
  
The previous set of steps sent data to the ALU. Next we will tell the ALU what to do with the data. 

In the bottom right of the simulator is yet another knob entitled `ALU Operation.` This knob instructs the ALU what operation to perform on the data it has received. 

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_4.png?raw=true" width="500"></p>

Click the knob so that it points to the instruction `A-B.`

The box to the left of the ALU knob is a diagnostic. It reports information based on the input provided to the ALU. Right now, `zero` has a check next to it because the default result is zero. You should see this reflected in the `C` textbox.

<blockquote>Q3: What do you think will happen to the boxes when the result is less than zero?</blockquote>

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_4.png?raw=true" width="500"></p>

Check that the simulator's current settings to make sure it is set to run `A-B`, where `A` is `R2` and `B` is `R1`.

<blockquote>Q4: With the values of <code>R1=42</code> and <code>R2=31</code> that you input earlier, what do you expect the result <code>C</code> to be?</blockquote>

Run the simulator to start a cycle with these settings. Halt the simulator when the result flashes in `C.` 

<blockquote>Q5: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?</blockquote>

Now we want the ALU to do something with the calculated result. 

The calculated result gets sent along the `C bus` back into the `register bank`. The `C Bus Address` knob in the top-left of the simulator tells the CPU which register it should use to store the calculated result. 

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_5.png?raw=true" width="500"></p>

Click the knob to store the result in `R3`. Run a simulation of a full cycle to subtract `R1` from `R2` and store the result in `R3`.

<blockquote>Q6: Describe what happened and the output in the previous step.</blockquote>

<blockquote>Q7: What settings (e.g., knob positions) would cause the value stored in <code>R3</code> to be doubled?</blockquote>

<blockquote>Q8: Set <code>R3</code> to 12 and test your answer to Q7? Did your hypothesis hold true? Why or why not?</blockquote>

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

So far, we have only been using data from a limited number of CPU registers. Actual computers have much more storage in their main memory. Data gets from memory into the registers through additional communication channels.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_6.png?raw=true" width="500"></p>

Open the [Knob & Switch Datapath and Memory Simulator](http://www.dave-reed.com/book/Chapter14/dpandmem.html) in a new browser window. 

Two notable components here are the memory and bus switches. The memory values on the left of the simulator represent `RAM`. The button next to each memory location indicates which location will be read (`R`) from or written to (`W`) in one cycle of the machine.

The bus connections from the ALU to the register bank now have switches on them. You can click these connections to toggle (open and close) the switches. Note that an open switch looks like an open door. No signal will flow across an open switch. A closed switch allows the signal to flow across it. 

We also have two new connections along the `C bus`. The `C bus` is the pathway into the register bank. The connection pointing up from the `Main Memory Bus` into `C bus` allows us put memory values into registers, rather than ALU results. 

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_7.png?raw=true" width="500"></p>

Open the circuit from the ALU into the `C bus`, so that there is no longer a connection.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_8.png?raw=true" width="500"></p>

Click to close the connection from the `Main Memory bus` to the `C bus`. The connection from the `C bus` to the memory bus should be open.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_9.png?raw=true" width="500"></p>

Put the value `42` into memory location `0`, and select it as the `RW` location.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_10.png?raw=true" width="500"></p>

Set the connection switch along the `C Bus` into the register bank so that it is closed. Select the `C Bus address` to be `R0`.

<blockquote>Q9: Based on these settings, what do you think will happen when you click <code>Execute</code>?</blockquote>
  
<blockquote>Q10: Test your prediction using the simulator. Did your hypothesis hold true? Why or why not?</blockquote>

<blockquote>Q11: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?</blockquote>

<blockquote>Q12: Set <code>R0 = 23</code> and <code>R3 = 16</code> to test your Q11 answer. Did your hypothesis hold true? Why or why not?</blockquote>

# Assembly Language

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=bae0c40a-1e2d-43bc-b27c-aef40109b060">Assembly Language</a></td>
  </tr>
  </table>

## Key Terms

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

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLScQoRbyDYB2Cisg_AmfMhUqj8qXn0ZbeuembRhQpOnbb64I2g/viewform?usp=sf_link">Assembly Language Comprehension Check</a></td>
  </tr>
  </table>

what type of info is in an instruction

Relationship of machine/assembly language

What kinds of asks can assembly language "do"

## Application

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_11.png?raw=true" width="500"></p>

Open the [Knob & Switch Machine Language Instruction Set](http://www.dave-reed.com/book/Chapter14/instructions.html) in a new browser window. Open the [Knob & Switch Machine Simulator](http://www.dave-reed.com/book/Chapter14/machine.html) in a second new browser window. Keep both Knob & Switch windows open in this section of the lab.

We're going to use the simulator and instruction set to run the program outlined in the "Assembly Language" lecture segment.

This simulator has its own labeling system, and assembly language is machine-specific, so the instruction set will be needed.

The core tasks for this program:
- Read memory location `14` into `R0` (the first register)
- Read memory location `15` into `R1` (the second register)
- Add the two register values and store in `R1` (second register)
- Store the arithmetic operation output in memory location `13`

<blockquote>Q13: How would we represent each of these tasks using this simulator's assembly code? HINT: Think through the underlying program logic and connect to examples in the instruction set.</blockquote>

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Main_Memory.png?raw=true" width="500"></p>

Let's put each of these instructions in a main memory location.
- Main memory location #0: Read memory location `14` into `R0` (the first register)
- Main memory location #1: Read memory location `15` into `R1` (the second register)
- Main memory location #2: Add the two register values and store in `R1` (second register)
- Main memory location #3: Store the arithmetic operation output in memory location `13`

Since our first two instructions involve reading values from memory, we'll need to add values to main memory locations `14` and `15`. 
- Value for `14`: `3`
- Value for `15`: `14`

We don't need to make any other changes to the simulator (circuits, knobs, etc).

<blockquote>Q14: Based on these settings, what do you think will happen when you run this program? Use the fetch-execute cycle framework to describe what will happen in each iteration of the program.</blockquote>

Fetch-execute cycle:
- Fetch instruction
- Decode instruction
- Get data (if needed)
- Execute instruction

<blockquote>Q15: When will this program stop or end?</blockquote>

<blockquote>Q16: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?</blockquote> 

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Control_Unit.png?raw=true" width="500"></p>

<blockquote>Q17: What can you tell about how the simulator's control unit is interpreting the assembly language instructions? NOTE: You do not need to map out the exact assembly-machine language translation. Describe in general how assembly language instructions are handled by the control unit.</blockquote>

Think about how many discrete instructions are part of this program. Since there are only four instructions, the simulator should only need 4 cycles to finish the program.

But you may have noticed the program is still running and the `PC` (program counter) value continues to increase.

<blockquote>Q18: What settings or values would we need to modify for the program to stop after executing the last instruction?</blockquote>

<blockquote>Q19: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?</blockquote> 

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

<blockquote>Q20: How would you describe some of these specifications in your own words, using terms and concepts covered in this lab?</blockquote>

You may be wondering if these specifications matter for your regular computer use. That's a fair question. 

Your computer's input devices control what types of devices you can connect to the computer, from the number and type of USB ports to HDMI connections and other adapters.

Your computer's output devices, especially the display, control screen size, resolution, and other aspects of the visual interface.

Sometimes, operating system updates can run into compatibility issues with the underlying computer hardware. For example, the hardware in Professor Walden's second-generation iPad stopped supporting iOS updates in 2016, meaning the tablet isn't able to run current versions of most apps or programs. Mac operating system updates often have specific hardware requirements and [can only be rolled out on select models](https://support.apple.com/en-us/HT212551). The recent Windows 11 roll out has very specific minimum system requirements.

Learn more about the Windows 11 rollout:
- [Windows](https://blogs.windows.com/windows-insider/2021/08/27/update-on-windows-11-minimum-system-requirements-and-the-pc-health-check-app)
- [CNet](https://www.cnet.com/tech/services-and-software/microsofts-strict-windows-11-device-requirements-have-one-exception-what-to-know)

# Lab Notebook Questions

[Link to lab notebook template](https://docs.google.com/document/d/1SpHmyZkN7b5wmtY0n8y5jI6JxBanZXg8UVZOoNPIv_o/copy) (ND users, Google Doc)
- Simulator screenshots are HIGHLY recommended.
  * Windows ([Snipping Tool](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b) for folks running older versions of Windows; [Snip & Sketch](https://www.lifewire.com/snip-and-sketch-windows-10-4774799) for folks running updated versions)
  * [Mac](https://support.apple.com/en-us/HT201361)
  * [Google Chromebook](https://support.google.com/chromebook/answer/10474268?hl=en)
- [Tutorial for adding images/tables/drawings to a Google Doc](https://www.techrepublic.com/article/how-to-add-images-tables-and-drawings-to-a-google-doc-file/)

Q1: Based on these bus settings, what values do you expect to show along the A and B bus?

Q2: What happens when you click <code>Execute</code>? Are the <code>A bus</code> and <code>B bus</code> values what you expected? Why or why not?
  
Q3: What do you think will happen to the boxes when the result is less than zero?

Q4: With the values of <code>R1=42</code> and <code>R2=31</code> that you input earlier, what do you expect the result <code>C</code> to be?

Q5: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?

Q6: Describe what happened and the output in the previous step.

Q7: What settings (e.g., knob positions) would cause the value stored in <code>R3</code> to be doubled?

Q8: Set <code>R3</code> to 12 and test your answer to Q7? Did your hypothesis hold true? Why or why not?

Q9: Based on these settings, what do you think will happen when you click <code>Execute</code>?
  
Q10: Test your prediction using the simulator. Did your hypothesis hold true? Why or why not?

Q11: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?

Q12: Set <code>R0 = 23</code> and <code>R3 = 16</code> to test your Q11 answer. Did your hypothesis hold true? Why or why not?

Q13: How would we represent each of these tasks using this simulator's assembly code? HINT: Think through the underlying program logic and connect to examples in the instruction set.

Q14: Based on these settings, what do you think will happen when you run this program? Use the fetch-execute cycle framework to describe what will happen in each iteration of the program.

Fetch-execute cycle:
- Fetch instruction
- Decode instruction
- Get data (if needed)
- Execute instruction

Q15: When will this program stop or end?

Q16: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?

Q17: What can you tell about how the simulator's control unit is interpreting the assembly language instructions? NOTE: You do not need to map out the exact assembly-machine language translation. Describe in general how assembly language instructions are handled by the control unit.

Q18: What settings or values would we need to modify for the program to stop after executing the last instruction?

Q19: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?

Q20: Find the hardware specs for your personal computer (or a school computer you can access). How would you describe some of these specifications in your own words, using terms and concepts covered in this lab?

- [Mac users](https://support.apple.com/guide/system-information/get-system-information-syspr35536/mac)
- [PC users](https://www.lifewire.com/how-to-get-your-computer-specs-3506998)
- [Chromebook](https://www.lifewire.com/how-to-check-chromebook-specs-hardware-4782658)
- [Linux](https://www.makeuseof.com/check-system-details-and-hardware-information-on-linux/)
