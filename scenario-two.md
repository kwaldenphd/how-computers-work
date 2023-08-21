# How Computers Work (Part 1): Scenario #2 (ALU & Memory)

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

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

<blockquote>Q8: Based on these settings, what do you think will happen when you click <code>Execute</code>?</blockquote>
  
<blockquote>Q9: Test your prediction using the simulator. Did your hypothesis hold true? Why or why not?</blockquote>

<blockquote>Q10: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?</blockquote>

<blockquote>Q11: Set <code>R0 = 23</code> and <code>R3 = 16</code> to test your Q11 answer. Did your hypothesis hold true? Why or why not?</blockquote>
