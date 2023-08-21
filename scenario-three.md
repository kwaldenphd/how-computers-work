# How Computers Work (Part 1): Scenario #3 (ALU & Memory)

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

<p align="center"><img align="center" src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Fig_11.png?raw=true" width="500"></p>

Open the [Knob & Switch Machine Language Instruction Set](http://www.dave-reed.com/book/Chapter14/instructions.html) in a new browser window. Open the [Knob & Switch Machine Simulator](http://www.dave-reed.com/book/Chapter14/machine.html) in a second new browser window. Keep both Knob & Switch windows open in this section of the lab.

We're going to use the simulator and instruction set to run the program outlined in the "Assembly Language" lecture segment.

This simulator has its own labeling system, and assembly language is machine-specific, so the instruction set will be needed.

The core tasks for this program:
- Read memory location `14` into `R0` (the first register)
- Read memory location `15` into `R1` (the second register)
- Add the two register values and store in `R1` (second register)
- Store the arithmetic operation output in memory location `13`

<blockquote>Q1: How would we represent each of these tasks using this simulator's assembly code? HINT: Think through the underlying program logic and connect to examples in the instruction set.</blockquote>

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

<blockquote>Q2: Based on these settings, what do you think will happen when you run this program? Use the fetch-execute cycle framework to describe what will happen in each iteration of the program.</blockquote>

Fetch-execute cycle:
- Fetch instruction
- Decode instruction
- Get data (if needed)
- Execute instruction

<blockquote>Q3: When will this program stop or end?</blockquote>

<blockquote>Q4: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?</blockquote> 

<p align="center"><img src="https://github.com/kwaldenphd/how-computers-work/blob/main/images/Control_Unit.png?raw=true" width="500"></p>

<blockquote>Q5: What can you tell about how the simulator's control unit is interpreting the assembly language instructions? NOTE: You do not need to map out the exact assembly-machine language translation. Describe in general how assembly language instructions are handled by the control unit.</blockquote>

Think about how many discrete instructions are part of this program. Since there are only four instructions, the simulator should only need 4 cycles to finish the program.

But you may have noticed the program is still running and the `PC` (program counter) value continues to increase.

<blockquote>Q6: What settings or values would we need to modify for the program to stop after executing the last instruction?</blockquote>

<blockquote>Q7: Test your prediction using the simulator. What parts of your hypothesis held true? What parts did not?</blockquote> 
