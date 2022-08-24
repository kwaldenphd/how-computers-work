# Key Terms

**Addressing Mode**
- Typically 3 bits. It indicates how to interpret the operand specifier.

**Arithmetic Logic Unit**
- "An arithmetic logic unit (ALU) is a combinational digital electronic circuit that performs arithmetic and bitwise operations on integer binary numbers" ([Wikipedia](https://en.wikipedia.org/wiki/Arithmetic_logic_unit))

**Assembler**
- "An assembler program creates object code by translating combinations of mnemonics and syntax for operations and addressing modes into their numerical equivalents. This representation typically includes an operation code ('opcode') as well as other control bits and data. The assembler also calculates constant expressions and resolves symbolic names for memory locations and other entities" ([Wikipedia](https://en.wikipedia.org/wiki/Assembly_language#Assembler))

**Assembly Language**
- "In computer programming, assembly language...is any low-level programming language with a very strong correspondence between the instructions in the language and the architecture's machine code instructions. Assembly language usually has one statement per machine instruction (1:1)...Because each assembly depends on the machine code instructions, each assembly language is specific to a paticular computer architecture" ([Wikipedia](https://en.wikipedia.org/wiki/Assembly_language))

**Bus**
- "In computer architecture, a bus…is a communication system that transfers data between components inside a computer, or between computers. This expression covers all related hardware components (wire, optical fiber, etc.) and software" ([Wikipedia](https://en.wikipedia.org/wiki/Bus_(computing)))

**CPU**
- "A central processing unit (CPU), also called a central processor or main processor, is the electronic circuitry within a computer that executes instructions that make up a computer program. The CPU performs basic arithmetic, logic, controlling, and input/output (I/O) operations specified by the instructions…Principal components of a CPU include the arithmetic logic unit (ALU) that performs arithmetic and logic operations, processor registers that supply operands to the ALU and store the results of ALU operations, and a control unit that orchestrates the fetching (from memory) and execution of instructions by directing the coordinated operations of the ALU, registers and other components" ([Wikipedia](https://en.wikipedia.org/wiki/Central_processing_unit))

**Fetch-Execute Cycle**
- Computer processing cycle that includes four main steps:
  * Fetch instruction
  * Decode instruction
  * Get data (if needed)
  * Execute instruction

**Input and Output (I/O)**
- I/O devices provide inputs to the system and enable the computer to provide output
- Input device examples: keyboard, mouse, network card, etc.
- Output device examples: monitor, display, printer, etc.

**Instruction Register (IR)**
- Register with the instruction that is currently being executed

**Instruction Specifier**
- Typically the first byte of an instruction. If present, it indicates which operation is being performed. Also tells the computer how to process the operand.

**Memory**
- "In computing, memory refers to a device that is used to store information for immediate use in a computer or related computer hardware device" ([Wikipedia](https://en.wikipedia.org/wiki/Computer_memory))

**Persistent Memory**
- Physical storage (magnetic disks, solid state disks, magnetic tape, etc) that retains information even when the device is powered off

**Processor (or processing unit)**
- "In computing, a processor or processing unit is an electronic circuit which performs operations on some external data source, usually memory or some other data stream. The term is frequently used to refer to the central processor (central processing unit)" ([Wikipedia](https://en.wikipedia.org/wiki/Processor_(computing))

**Operand Specifier**
- Typically the second and third bytes in an instruction. If present, it can hold the operand or its address (location).

**Operation Codes (opcodes)**
- Typically 4-8 bits. It indicates the instruction specifier format and can include a register specifier.

**Random Access Memory (RAM)**
- "Random-access memory (RAM) is a form of computer memory that can be read and changed in any order, typically used to store working data and machine code" ([Wikipedia](https://en.wikipedia.org/wiki/Random-access_memory))
- RAM is controlled by the CPU and can include data and instructions

**Registers**
- "In computer architecture, a processor register is a quickly accessible location available to a computer's central processing unit (CPU). Registers usually consist of a small amount of fast storage" ([Wikpedia](https://en.wikipedia.org/wiki/Processor_register))

**Von Neumann Architecture**
- Developed in the 1940s, this computer design framework is based on the principle that data and instructions have the same logical significance to the computer. Rather than separate data and instructions, the von Neumann architecture conceptualizes a computer system that is able to store instructions and data. This is referred to as a `stored-program computer`.
- The core components of the von Neumann architecture:
  * Input and output
  * Control unit
  * Arithmetic and logic unit (ALU)
  * Memory unit
    * The last three components (control unit, ALU, memory) make up the central processing unit (CPU) 
