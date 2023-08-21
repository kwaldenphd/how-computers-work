# How Computers Work (Part 1): Scenario #1 (ALU & Memory)

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>This tutorial was written by Katherine Walden and is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

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

<blockquote>Q6: What settings (e.g., knob positions) would cause the value stored in <code>R3</code> to be doubled?</blockquote>

<blockquote>Q7: Set <code>R3</code> to 12 and test your answer to Q7? Did your hypothesis hold true? Why or why not?</blockquote>
