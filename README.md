# Simple-TTL-CPU
A design and simulation of a simple 4-bit TTL CPU "Nybble" using H. Neeman's "Digital" simulator

This project aims to provide a series of step by step lessons on building a simple TTL cpu from scratch.

Instead of using real TTL chips, breadboards and jumper wires, the project will be introduced as a series of simulated circuits using H. Neeman's "Digital" simulator, which may be downloaded here:  https://github.com/hneemann/Digital

Once "Digital" has been installed, the user will be able to download and interact with the various .dig simulation files.

#Gate and Chip Level Design

"Digital" provides a convenient means of "breadboarding" logic circuits and then testing their behaviour. Circuits can be saved and used to form a custom library, which may be used within a heirarchical design.

The User may choose to design at a gate level - using nothing but Nand gates, in a similar fashion to the modules created in the "Nand to Tetris" online course. A complete computer can be designed form modules constructed entirely from Nand Gates.  The 16-bit "Hack" computer described in the "Nand to Tetris" course may be constructed from approximately 1600 Nand gates, not including memory.

If gate level design is not desirable, the "Digital" simulator contains a library of standard TTL integrated circuits and popular memory devices. Whilst these allow more rapid progress, the designer is constrained by the number of pins on a typical TTL package, and most functions are limited to a 4 or 8-bit width. This means that wider logic functions will need multiple TTL packages to implement often accompanied by not insignificant wiring.

#Understanding the Operation of a Simple CPU

For convenience a cpu can be subdivided into a series of functional modules, and these modules can be further subdivided down into a series of logic building blocks. If the User is suitably interested, the building blocks may be further analysed down to the individual gates. Each level of this analysis masks the underlying complexity of the layers below.

As an illustration, in a simple CPU, there may be 16 functional modules in the top layer. Each module may consist of between 1 and 10 commonly available ICs and each IC may consist of between 10 and 100 gates.

The size of the cpu is also dictated by the word size - the logic requires scales approximately as a linear function of the wordsize. 

A 4-bit machine may be implemented in around 20 ICs, an 8-bit machine in about 40 ICs and a 16-bit machine in about 80 ICs. This is not a hard and fast rule as it depends on the specifics of the machine. It is also possible to trade off hardware complexity against software complexity. In the 1960s when hardware was very expensive, minicomputers were designed to minimise the hardware, but at the expense of difficult programming and more effort required to write software.

A simple stored program computer may be defined by 5 fundamental modules:

Input
Output
Memory
Arithmetic & Logic
Control

These modules may be further expressed in terms of their function.  For example Input might be in the form of binary toggle switches on the front panel accompanied by LEDs or hex displays to indicate the output. With further complexity, text input and output might be provided from a serial terminal. From the late 1970s and the advent of home computers, input was from an array of some 40+ keyboard switches and output was in character and graphics form to a TV display or CRT monitor.

Memory is often referred to as ROM (permanent storage) or RAM (re-writeable storage). The architecture of the computer is defined either as Harvard or von Neumann, depending on how the cpu connects to the memory. The Harvard model has separate memory spaces to hold the program (ROM) and the data (RAM). The von Neuman model uses less hardware and both the program and the data are contained within the same program space. This hardware simplification leads to a reduction in performance as the von Neumann architecture cannot access both program and data simultaneously.

Memory can also exist in the form of storage registers, where temporary results or operands may be held locally without having to access the main memory. Early minicomputers had very few registers, because of the cost of their implementation in hardware. Instead, almost all cpu operations had to use main memory to store operands and results. 

The popular 6502, designed for low cost and complexity is an example of a microprocessor that uses very few (3) user registers. This was partly compensated for by allowing easy access to the "zero page" of RAM, where operands and results could be stored conveniently.

Most modern processors have a larger number of user registers:  PDP 11 (8), MSP430 (16), AVR (32). This allows greater flexibility in programming and is essential for efficient hosting of high level languages such as C.  





# Exercise 1. LEDS and Switches.

This creates a simple LED and Switch interface which allows the user to enter binary data using "toggle" switches and display the data on an array of single LEDs and also in hexadecimal form using the 7-segment display component.

In addition to the LEDs and switches, the lesson introduces the 7474 dual flip-flop and the 74173 quad flipflop, which will be used throughout the series to provide a 4-bit register.

The 7474 is used to toggle the switch input between it's two states. Press once and the state of the output will change.

The 74173 illustrates the use of a quad flipflop being used as a storage register. It introduces the use of the Hold/Load input, Master Clear, Clock and tri-state control.

The LED and switch circuit simulation is reminiscent of the "Front Panels" from the minicomputers of the 1960s and the very early home computer kits of the early 1970s, which used toggle switches and indicator lamps to enter data into the machine and read back numerical results.

# Exercise 2 Program Counter and Memory

In this exercise I introduce the Program Counter and the concept of Memory addressing. 

The program counter is constructed from a pair of common 74xx163 4-bit counters that are cascaded together to create an 8-bit counter. This could be further extended easily to 12 or even 16 bits.

On the receipt of a positive going clock pulse, the counter increments its total by 1.

The counter has four outputs Q0,Q1,Q2 and Q3 which will count up the 4-bit binary sequence 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15. On reaching 15 the "ripple carry output" is asserted which is used to increment the next 4-bit stage.

Each counter has 4 parallel load inputs. By setting these and asserting the /LD input, the counter will be preset to a given count. The counter will then continue to count upwards from the given count.

This is the mechanism that allows a stored program to be executed and jump from one location to another.

# Exercise 3 Arithmetic and Logic Unit ALU

This exercise introduces the Arithmetic Logic unit or ALU, which is initially presented as a 4-bit building block.

This design has been adapted from a design by Dieter Muller - a TTL computer enthusiast.

It is based entirely on combinational logic, with the outputs being defined solely by the logic levels applied to the inputs.

It allows a 4-bit ALU slice to be constructed from just 5 common TTL ICs. It uses four 74xx153 multiplexers to create the logic unit and a 4-bit adder 74xx283 to provide addition and subtraction.

This makes a very economical ALU capable of AND, OR, XOR, NOT, ADD, SUB, INC, DEC and NEG using readily available TTL devices.

It could always be reduced to logic look up tables stored in a 16K ROM, but this solution is likely to be simpler, cheaper and faster.

# Exercise 4 Instruction Decoder

This building block introduces the Instruction Decoder. It is used to convert one or more bit-fields of the instruction word and produces a set of control signals that are used to manipulate the hardware including the ALU, memory and registers.

In this design it takes the upper 4-bits from a byte in memory and decodes them into 16 individual instructions using a pair of 3-8 line decoders (74xx138) and a diode matrix. The diode matrix works as a primitive ROM.
 
When the 74138 lowers one of the horizontal selection signals, the presence of a diode in the matrix will pull down one of the corresponding vertical (output) signals. The 74540 is an octal inverter/driver which inverts the output from the diode matrix and sends it on to the ALU control inputs or wherever it is needed.
 
The diode matrix is a very cost effective of creating a small, and fairly fast ROM - in hardware. The idea was originally used in early desktop calculators in the late 1960s, - but this iteration has been borrowed from the Gigatron TTL computer.

The arrangement I have shown can be expanded to a 16 x 8-bit ROM.

Other recent progress a simplification of the Front Panel-Memory schematic and the inclusion of a 4-bit 74194 universal shift register in the ALU (instead of the 4-bit 74173 register) to allow left and right shifts.

# Exercise 5 Nybble

The file Nybble_6.dig combines the three main building blocks of the system.

There is sufficient circuitry to enter data from the front-panel switches into memory. 

The ALU can be controlled manually and shows the results of using either a plain register or a universal shift register as the Accumulator.

The Instruction Decoder allows efficient control of the ALU.


 


