# Simple-TTL-CPU
A design and simulation of a simple 4-bit TTL CPU "Nybble" using H. Neeman's "Digital" simulator

This project aims to provide a series of step by step lessons on building a simple TTL cpu from scratch.

Instead of using real TTL chips, breadboards and jumper wires, the project will be introduced as a series of simulated circuits using H. Neeman's "Digital" simulator, which may be downloaded here:  https://github.com/hneemann/Digital

Once "Digital" has been installed, the user will be able to download and interact with the various .dig simulation files.

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


 


