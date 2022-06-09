# Logic gates, digital circuits, data path, memory, and machine language

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

This lab covers a variety of topics related to how computers "work." This lab is designed to help you gain an understanding of how the basic logical and mathematical operations underlying computation are performed mechanically. We will also use a simulation of CPU architecture to learn more about how an instruction is processed along the CPU data path cycle and how values from memory are incorporated into CPU instructions. We are doing this to gain more experience with understanding a computer’s mechanical operations at a higher level of abstraction. Finally, this lab covers reading and writing basic machine language, to help us see the 0s and 1s underneath higher level programming and apply them to basic algorithms.

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=63a3251a-e1d0-4b36-b002-ad3d00cb609c">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=d55a3a86-9e99-4008-9e4f-ae510174ce65">Lecture/live coding playlist</a></td>
  </tr>
  </table>

## Acknowledgements

**Logic gates and digital circuits**
This section of the lab incorporates elements of the "Log gates & digital circuits" lab:
- Written: Marge M. Coahran, April 2008
- Revised: Jerod Weinman, 17 March 2009
- Revised: Marge Coahran, 14 April 2010
- Revised: Jerod Weinman, 22 March 2011 & 15 April 2011
- Revised: Jerod Weinman, 3 April 2014
- Revised: Jerod Weinman, 1 April 2015

**Data path and memory**
This section of the lab is based on the "Data path & memory" lab:
- Created: Jerod Weinman, 16 March 2009
- Modified: Jerod Weinman, 20 April 2011
- Modified: Jerod Weinman, 4 April 2014
- Portions adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.1-14.6.

**Machine language**
This section of the lab is based on the "Machine language" lab:
- Created: Jerod Weinman, March 16, 2009
- Revised: Janet Davis, April 27, 2012
- Revised: Janet Davis, March 12, 2013
- Revised: Jerod Weinman, 4 April 2014
- Adapted from Dave Reed, “A Balanced Introduction to Computer Science,” Exercises 14.9, 14.10, and 14.13. 

# Table of Contents

- [Lecture and Live Coding](#lecture-and-live-coding)
- [Lab Notebook Template](#lab-notebook-template)
- [Data path and memory](#data-path-and-memory)
  * [CPU Data Path](#cpu-data-path)
  * [ALU Operation](#alu-operation)
  * [CPU and memory](#cpu-and-memory)
- [Machine Language](#machine-language)
  * [Assembly to Machine Language](#assembly-to-machine-language)
  * [Machine to Assembly Language](#machine-to-assembly-language)
    * [Executing a Program](#executing-a-program)
    * [The `HALT` Instruction](#the-halt-instruction)
- [Working at the Command Line](#working-at-the-command-line)
- [OPTIONAL: Logic gates and digital circuits](#optional-if-interested-in-diving-more-into-circuits)
  * [Installing SmartSim](#installing-smartsim)
  * [Getting Started With SmartSim](#getting-started-with-smartsim)
- [Lab Notebook Questions](#lab-notebook-questions)

# Lecture and Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=63a3251a-e1d0-4b36-b002-ad3d00cb609c">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=d55a3a86-9e99-4008-9e4f-ae510174ce65">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Lab Notebook Template

[Link to lab notebook template](https://docs.google.com/document/d/1OvM0j6faXkaJAFmrTuKDjBB0aXdPyu3lqzdL37iIEGw/copy) (ND users, Google Doc)

# Data path and memory

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=63a3251a-e1d0-4b36-b002-ad3d00cb609c">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8c5bb81d-6381-48b7-806e-ad82016237db">How Computers Work</a></td>
  </tr>
  </table>

## CPU Data Path

1. Open the [Knob & Switch Datapath 1 Simulator](http://www.dave-reed.com/book/Chapter14/datapath/datapath.html) in a new browser window. 

2. This simple CPU contains four registers, but no control unit. You will be the control unit that directs which registers are operated on and which operations are done.

3. Take a look at the top box that says `Register Bank.` At the right are two command knobs, `A Bus Address` and `B Bus Address.` These knobs specify which registers should be read as inputs to the ALU. 

<blockquote>CPU stands for central processing unit. ALU stands for arithmetic logic unit.</blockquote>

4. Click on each knob to turn it.

5. Set the `A bus` address to `R2` and the `B bus` address to `R1`. 

6. When a cycle is executed, the CPU will send the values from `R2` and `R1` along the bus.

7. The register values are the textboxes with a green background. Currently, all the register default values are zero. 

8. Set the value of `R1` to 42. Set the value of `R2` to 31.

9. Check that `Animation Speed` is set on `Medium` and `Number Base` is set to `+-10.`

<blockquote>Q1: Based on the settings of the bus addresses, what values do you expect to show along the A and B bus?</blockquote>

<blockquote>Q2: What happens when you click Execute? Are the <code>A bus</code> and <code>B bus</code> values what you expected? Why or why not?</blockquote>
  
## ALU Operation

10. The previous set of steps sent data to the ALU. Next we will tell the ALU what to do with the data. 

11. In the bottom right of the simulator is yet another knob entitled `ALU Operation.` This knob instructs the ALU what operation to perform on the data it has received. 

12. Click the knob so that it points to the instruction `A-B.`

13. The box to the left of the ALU knob is a diagnostic. It reports information based on the input provided to the ALU.

14. Right now, `zero` has a check next to it because the default result is zero. You should see this reflected in the `C` textbox.

<blockquote>Q3: What do you think will happen to the boxes when the result is less than zero?</blockquote>

15. Check that the simulator's current settings to make sure it is set to run `A-B`, where `A` is `R2` and `B` is `R1`.

<blockquote>Q4: With the values of <code>R1=42</code> and <code>R2=31</code> that you input earlier, what do you expect the result <code>C</code> to be?</blockquote>

16. Run the simulator to start a cycle with these settings. Halt the simulator when the result flashes in `C.` 

<blockquote>Q5: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?</blockquote>

17. Now we want the ALU to do something with the calculated result.

18. The calculated result gets sent along the `C bus` back into the `register bank`.

19. The `C Bus Address` knob in the top-left of the simulator tells the CPU which register it should use to store the calculated result. 

20. Click the knob to store the result in `R3`.

21. Run a simulation of a full cycle to subtract `R1` from `R2` and store the result in `R3`.

<blockquote>Q6: Describe what happened and the output in the previous step.</blockquote>

<blockquote>Q7: What settings (e.g., knob positions) would cause the value stored in <code>R3</code> to be doubled?</blockquote>

<blockquote>Q8: Set <code>R3</code> to 12 and test your answer to Q7? Did your hypothesis hold true? Why or why not?</blockquote>

## CPU and memory

22. So far, we have only been using data from a limited number of CPU registers. Actual computers have much more storage in their main memory. Data gets from memory into the registers through additional communication channels.

23. Open the [Knob & Switch Datapath and Memory Simulator](http://www.dave-reed.com/book/Chapter14/dpandmem.html) in a new browser window. 

24. Two notable components here are the memory and bus switches. The memory values on the left of the simulator represent `RAM`. The button next to each memory location indicates which location will be read (`R`) from or written to (`W`) in one cycle of the machine.

25. The bus connections from the ALU to the register bank now have switches on them. 

26. Click these connections to toggle (open and close) the switches. Note that an open switch looks like an open door. No signal will flow across an open switch. A closed switch allows the signal to flow across it. 

27. Open the circuit from the ALU into the `C bus`, so that there is no longer a connection.

28. We also have two new connections along the `C bus`. The `C bus` is the pathway into the register bank. 

29. The connection pointing up from the `Main Memory Bus` into `C bus` allows us put memory values into registers, rather than ALU results. 

30. Click to close the connection from the `Main Memory bus` to the `C bus`. The connection from the `C bus` to the memory bus should be open.

31. Put the value 42 into memory location 0, and select it as the `RW` location.

32. Set the connection switch along the `C Bus` into the register bank so that it is closed. Select the `C Bus address` to be `R0`.

<blockquote>Q9: Based on these settings, what do you think will happen when you click Execute?</blockquote>
  
33. Verify your prediction using the simulator.

<blockquote>Q10: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?</blockquote>

34. Set `R0=23` and `R3=16` and verify your prediction using the simulator.

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSfsUlpypqX9m1TS5Rz074AHlWcLJxJlmhzDtLwve9gXJPkIKg/viewform?usp=sf_link">How Computers Work Lecture Check-In</a></td>
  </tr>
  </table>

# Machine Language

35. Open the [Knob & Switch Machine Language Instruction Set](http://www.dave-reed.com/book/Chapter14/instructions.html) in a new browser window. 

36. Open the [Knob & Switch Machine Simulator](http://www.dave-reed.com/book/Chapter14/machine.html) in a second new browser window. 

37. Keep both Knob & Switch windows open in this section of the lab.

## Assembly to Machine Language

38. In memory location `0`, type the instruction `ADD R2 R1 R0`.

<blockquote>Q11: Using the Instruction Set from step 35, how would you start translating the ADD R2 R1 R0 instruction from assembly (or instructional language) to binary language (or machine language)?</blockquote>

39. Use the `View As:` drop-down menu on the left-hand side of the window to check your result. Change the menu value to `2` to reveal the binary executable instruction. 

<blockquote>Q12: How does your answer to Q11 compare to the simulator output from step 39? What discrepancies (if any) can you identify?</blockquote>

## Machine to Assembly Language

40. Refresh the window to reset the simulator to default settings.

41. On the drop-down menu next to memory location `1`, change the value from `Auto` to `2`.

<blockquote>Q13: Using the Instruction Set from step 35, how would you start to translate the binary instruction (or machine code) 1000001001001010 into assembly language or instructional language?</blockquote>

42. Copy this bit string into memory location `1`.

43. On the drop-down menu next to memory location `1`, change the value from `2` to `Instr` to show the binary executable instruction. 

<blockquote>Q14: How does your answer to Q13 compare to the simulator output from step 43? What discrepancies (if any) can you identify?</blockquote>

### Executing a Program

44. Enter the `HALT` instruction in memory location `2`.

45. Change the contents of `R0`, `R1`, `R2`, and `R3` to 1, 3, 5, and 7, respectively.

46. Click `Reset` above the `PC` (Program Counter) to initialize it to zero.

<blockquote>Q15: What do you expect to be the result when you click Execute? Run the simulation and verify your prediction.</blockquote>
  
### The `HALT` Instruction

<blockquote>Q16: What would happen if you had forgotten the <code>HALT</code> instruction? How would the control unit react?</blockquote>

47. Test your prediction by changing `HALT` in memory address `2` to something other than the default value.
  * You may need to change the `View as` drop-down to something other than `Instr`.

48. Reset the PC to value zero and execute the program to test your prediction.
 
# Working at the Command Line

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=879d98fd-b758-412a-982b-ad3d00c65d52">Command Line Interface</a></td>
  </tr>
  </table>

 *The Programming Historian* is a multi-language, peer-reviewed online resource with "novice-friendly, peer-reviewed tutorials that help humanists learn a wide range of digital tools, techniques, and workflows to facilitate research and teaching" (["The Programming Historian"](https://programminghistorian.org/))
 
For the last part of this lab, we will work through an adapted version of the "[Introduction to the Bash Command Line](https://programminghistorian.org/en/lessons/intro-to-bash)" lesson, to apply the concepts covered in the "Bite Size Command Line" zine.
- Ian Milligan and James Baker, "Introduction to the Bash Command Line," The Programming Historian 3 (2014), https://doi.org/10.46430/phen0037.
 
The text content below is adapted from the *PH* lesson as well as Miriam Posner's "[Getting Started With Unix](https://github.com/miriamposner/unix/blob/main/getting_started_with_commandline.md)" tutorial.

The usual way that computer users today interact with their system is through a Graphical-User Interface, or GUI. This means that when you go into a folder, you click on a picture of a file folder; when you run a program, you click on it; and when you browse the web, you use your mouse to interact with various elements on a webpage. Before the rise of GUIs in the late 1980s, however, the primary way to interact with a computer was through a command-line interface [CLI].

Command-line interfaces have advantages for computer users who need more precision in their work – such as digital historians. They allow for more detail when running some programs, as you can add modifiers to specify exactly how you want your program to run. Furthermore, they can be easily automated through scripts, which are essentially recipes of text-based commands.

There are two main command-line interfaces, or "shells." On OS [Mac] or many Linux installations, the shell is known as `bash`, or the ‘Bourne-again shell.’ For users on Windows-based systems, the command-line interface is by default `MS-DOS-based`, which uses different commands and syntax, but can often achieve similar tasks. This tutorial provides a basic introduction to the `bash` terminal, and Windows users can follow along by installing popular shells such as Cygwin or Git Bash [details and instructions provided below].

### For Windows Users

For Mac users (and most Linux installations), you’re in luck — you already have a bash shell installed. 

Windows users will need to take one extra step and install Git Bash. 
- Download the most recent ‘Full installer’ at [this page](https://git-for-windows.github.io)
- Instructions for installation are available at [Open Hatch](https://web.archive.org/web/20190114082523/https://openhatch.org/missions/windows-setup/install-git-bash)

## Opening Your Shell

*NOTE: The following screenshots show the Mac OS terminal/shell. Folks with other operating systems should still be able to follow the procedural steps.*

<p><figure><img align="center", src="https://programminghistorian.org/images/intro-to-bash/Terminal.png" alt="Image of Mac Shell icon">
 <figcaption>The Terminal.app program on OS </figcaption></figure></p>
 
Mac:
- By default, the shell is located in `Applications -> Utilities -> Terminal`

Windows:
- Run Git Bash from the directory that you installed it in. You will have to run it as an administrator - to do so, right click on the program and select 'Run as Administrator.'

<p><figure><img align="center", src="https://programminghistorian.org/images/intro-to-bash/Blank-Terminal.png" alt="Image of Mac Shell">
 <figcaption>A blank terminal screen on an OS workstation</figcaption></figure></p>
 
When the terminal or shell is running, you will see a window that looks similar to the image above.

<p><figure><img align="center", src="https://programminghistorian.org/images/intro-to-bash/Settings.png" alt="Image of Mac terminal settings">
 <figcaption>The Settings Screen on the OS X Terminal Shell Application</figcaption></figure></p>
 
For Mac users who want to customize the terminal's visual appearance:
- Open the `Settings` menu (in `Preferences`, under `Terminal`)
- Click the `Settings` tab to change the color scheme

Windows users can right-click on the application's top bar and select `Properties` to open the `Properties` tab.

## Terminal Wayfinding

<p><img align="center", src="https://raw.githubusercontent.com/miriamposner/unix/main/steps-getting_started_with_unix/step-1.jpeg" alt="Image of Mac shell"></p>

*NOTE: The following text and images are adapted from UCLA faculty member Miriam Posner's "[Getting Started With Unix](https://github.com/miriamposner/unix/blob/main/getting_started_with_commandline.md)" tutorial*

This is a terminal window, also called a `shell`. 

The active cursor showing up in the window is a `command prompt`. This is where you will type commands or instructions.

First, we can check your username using the `whoami` command.

Type `whoami` in the shell and hit the `Enter` or `Return` key.

The terminal returns your username.

The terminal's command prompt is ready for another command or instruction.

Let's try another command- this type, we'll use `echo` to repeat a set of characters in quotation marks.

Type `echo 'Hello world!' into the terminal and hit the 'Enter' or 'Return' key.

The `echo` command instructs the terminal to repeat whichever characters you include in the quotation marks.

## Typing Commands in the Terminal

You may have already noticed you're not able to navigate the terminal using your mouse or cursor.

We can navigate the terminal using the keyboard.

The `up` and `down` arrow keys let you move back (up) and forward (down) through previously typed commands. 

The `left` and `right` arrow keys let you move within characters or symbols for a specific command.

Press the `up` arrow once to show the previously-typed `echo` command.

Then, use the `left` and `right` arrow keys to navigate to the characters within the quotation marks and replace them with another word or phrase of your choosing.

Press `Return` or `Enter` to run the modified command. 

A couple other useful navigation tools:
- Press `Control` + `A` to move to the start of a line
- Press `Control` + `E` to move to the end of a line
- Type `clear` into the terminal and press `Return`/`Enter` to clear the screen
- When you're ready to close the terminal window, type `exit` and press `Return`/`Enter`

<p><img align="center", src="https://raw.githubusercontent.com/miriamposner/unix/main/steps-getting_started_with_unix/step-17.jpeg" alt="Diagram illustrating terminal syntax"></p>

A couple notes on terminal syntax:
- `commands` tell the computer to perform an action 
- `options` modify the command and use a hyphen (`-`) symbol
  * Sometimes `options` are called `flags` or `switches`
- `arguments` specify what the command operation will be performed on (i.e. a specific file or directory)

Not all commands require arguments or options, but some commands can have one or more of each.

You can also chain multiple commands together using the vertical bar `|` symbol. This is often called a `pipe`.

## Navigating Your File System

Before we start moving around, let's use the `pwd` (print working directory` command to show your current location.

Type `pwd` in the terminal and press `Enter` or `Return`.

Your output might look something like this:
```
/Users/kwalden
```

This directory information is called a `path` (sometimes called a `file path` when dealing with specific files).
- The backslash `/` at the start of the path stands for your computer's `root`
- Subsequent slashes indicate subfolders or subdirectories

So in the `/Users/kwalden` example, the terminal is running in the `kwalden` subfolder which is located in the `Users` folder. The `Users` folder is located at my computer's `root`.

<p><img align="center", src="https://raw.githubusercontent.com/miriamposner/unix/main/steps-getting_started_with_unix/step-4.jpeg" alt="Diagram illustrating computer directory structure"></p>

The inverted tree diagram shown above shows one example of a computer's file system.
- The `root` (top of the tree) is your computer's hard drive.
- The next set of branches are a set of folders (`directories`) that are used by everyone who uses the computer
- The `users` folder includes different specific user profiles
- The folders located under a specific username are associated with that user profile
  * These folders commonly include `Applications`, `Desktop`, `Documents`, `Downloads`, etc.

If you have ever used `File Explorer` (Windows) or `Finder` (Mac), you have navigated this tree structure using the graphical user interface (GUI).

Now let's think about how we navigate this structure using the command line interface (CLI).

### `ls`

Typically by default, your terminal will open in the folder or directory for your user profile.
- But you can check this using the `pwd` (print working directory) command

Let's see what other files and subdirectories are located in your current path by using the list command (`ls`).

Type `ls` in the terminal and press `Enter`/`Return`.

<p><img align="center", src="https://raw.githubusercontent.com/miriamposner/unix/main/steps-getting_started_with_unix/step-6.jpeg" alt="Terminal screenshot showing directory contents"></p>

Items that are followed by a file extension (e.g. `.docx`, `.txt`, `.xlsx`, etc) are generally individual files. Items that do not have a file extension are typically subfolders or subdirectories.

### `cd`

We can move down the tree using the `change directory` command (`cd`).

Let's move from your user profile folder to the Desktop.

Type `cd Desktop` and press `Enter`/`Return`.
- You can also type `cd Desk` and press the `Tab` key (before `Enter`/`Return`) to autocomplete the command

When using the `cd` (change directory) command, we are navigating the computer's file system using `relative paths`. This means the location information we are specifying in the terminal is relative to our current position or location in the file system. 

The previous `cd Desktop` command is an example of a relative path.

`Absolute paths` always start at the `root` and use backslash `/` symbols to indicate subfolders.
- `/Users/kwalden/Desktop` would be the absolute path version of the previous command
- NOTE: Be sure to replace `kwalden` with your user name

We can use the `ls` command again to see the materials located on our Desktop.

We can also move back up the file system tree using the `cd` command.

Instead of using `cd`  followed by a relative or absolute path, we can use `cd ..` (`cd` followed by a space and two periods) to move up one level in the tree.

Type `cd ..` in the terminal and press `Enter`/`Return`. You can test using `pwd` if needed, but you should be back in the specific user profile folder.

## Additional Resources

If you want to further explore command line syntax:
- Software Carpentries, "[The Unix Shell](https://swcarpentry.github.io/shell-novice/)" lesson
- Mary Brent, "[Linux Command Cheat Sheet](https://www.guru99.com/linux-commands-cheat-sheet.html)", *Guru99* (28 May 2022)
- Ian Milligan and James Baker, "Introduction to the Bash Command Line," The Programming Historian 3 (2014), https://doi.org/10.46430/phen0037.
- Miriam Posner, "[Getting Started With Unix](https://github.com/miriamposner/unix/blob/main/getting_started_with_commandline.md)" tutorial

<blockquote>Q17: Going back to our work with navigating the command line, open a Terminal on your laptop or desktop. Describe what you see.</blockquote>

<blockquote>Q18: When you use the ls -l command (lower-case letter l, lower-case letter s, space, dash, lower-case letter l), can you decipher the information that is displayed? Watch https://youtu.be/exQNuYxqFpA to help decode the information.</blockquote>

<blockquote>Q19: Take a few moments to reflect on your experience working in the command line. How does your navigation of the computer at the command line compare other ways of navigating a computer’s user interface?</blockquote>

<table>
 <tr><td>
<img src="https://www.freeiconspng.com/thumbs/survey-icon/survey-icon-12.png" alt="Clipboard icon" width="50"/></td>
  <td><a href="https://docs.google.com/forms/d/e/1FAIpQLSdq6gyJ26OLOWUVG4c1HVhiXPz3Q0b68Gqv1r0qfQhSR0zW9Q/viewform?usp=sf_link">Operating Systems Lecture Check-In</a></td>
  </tr>
  </table>

# OPTIONAL: If interested in diving more into circuits

## Logic gates and digital circuits

### Installing SmartSim 

A. There are a few free software options that simulate building circuits. One option for PC and Linux users is [called SmartSim](https://smartsim.org.uk/index.php?page=downloads), "a free and open source digital logic circuit design and simulation package.” SmartSim is released under a GNU General Public License Version 3.

B. Open a Terminal window and use `sudo apt-get update` and `sudo apt-get install smartsim` to install SmartSimP.

C. Open SmartSim.

### Getting Started With SmartSim

D. Work through the [SmartSim User Manual](https://smartsim.org.uk/downloads/manual/smartsim_user_manual.pdf) (or documentation for another circuit program) to become familiar with the program interface and explore various functions. [CircuitLab](https://www.circuitlab.com/docs/the-basics/) is another option that runs in a web browser and will work across operating systems. See also: CNET's ["Circuit Simulator on Mac" article](https://www.cnet.com/forums/discussions/circuit-simulator-on-mac/) (25 August 2016). 

E. After working through the documentation, attempt the following tasks:
  * add an input switch
  * add wires to your circuit
  * move or reposition circuit elements
  * delete wires from your circuit
  * add an output pin (LED) 
  * connect your input switch to the LED
  * use the input switch to turn the LED on and off
  * add an `AND-Gate` to your circuit
  * connect two input switches to the `AND-Gate`'s input points
  * connect an LED to the `AND-GATE`'s output point.
  * test all possible input combinations
  * add an `OR-Gate` and `NOT-gate` 
  * test inputs for these new gates

<blockquote>Describe your experience attempting each of tasks, relying on the documentation provided in the user manual. What went well? What was challenging? What lingering questions do you have about how circuits work? Include an image of your circuit.</blockquote>

# Lab Notebook Questions

All of the required questions are listed here for you to reference. Be sure to answer each question completely, including an explanation of how you arrived at your answer.
 
[Link to lab notebook template](https://docs.google.com/document/d/1OvM0j6faXkaJAFmrTuKDjBB0aXdPyu3lqzdL37iIEGw/copy) (ND users, Google Doc)
  
Q1: Based on the settings of the bus addresses, what values do you expect to show along the A and B bus?

Q2: What happens when you click Execute? Are the `A bus` and `B bus` values what you expected? Why or why not?

Q3: What do you think will happen to the boxes when the result is less than zero?

Q4: With the values of `R1=42` and `R2=31` that you input earlier, what do you expect the result `C` to be?

Q5: Is the result what you expected? Why or why not? What happened to the diagnostic boxes?

Q6: Describe what happened and the output in the previous step.

Q7: What settings (e.g., knob positions) would cause the value stored in `R3` to be doubled?

Q8: Set `R3` to 12 and test your answer to Q7? Did your hypothesis hold true? Why or why not?

Q9: Based on these settings, what do you think will happen when you click Execute?

Q10: What settings (bus addresses, ALU operation, switches, and memory RW) would result in R0 minus R3 being stored in memory location 4?

Q11: Using the Instruction Set from step 35, how would you start translating the ADD R2 R1 R0 instruction from assembly (or instructional language) to binary language (or machine language)?

Q12: How does your answer to Q11 compare to the simulator output from step 39? What discrepancies (if any) can you identify?

Q13: Using the Instruction Set from step 35, how would you start to translate the binary instruction (or machine code) 1000001001001010 into assembly language or instructional language?

Q14: How does your answer to Q13 compare to the simulator output from step 43? What discrepancies (if any) can you identify?

Q15: What do you expect to be the result when you click Execute? Run the simulation and verify your prediction.

Q16: What would happen if you had forgotten the `HALT` instruction? How would the control unit react?
 
Q17: Going back to our work with navigating the command line, open a Terminal on your laptop or desktop. Describe what you see. 

Q18: When you use the ls -l (lower-case letter l, lower-case letter s, space, dash, lower-case letter l) command, can you decipher the information that is displayed? Watch https://youtu.be/exQNuYxqFpA to help decode the information.

Q19: Take a few moments to reflect on your experience working in the command line. How does your navigation of the computer at the command line compare other ways of navigating a computer’s user interface?
