# Simple-TTL-CPU
A design and simulation of a simple TTL CPU using H. Neeman's "Digital" simulator

This project aims to provide a series of step by step lessons on building a simple TTL cpu from scratch.

Instead of using real TTL chips, breadboards and jumper wires, the project will be introduced as a series of simulated circuits using H. Neeman's "Digital" simulator, which may be downloaded here:  https://github.com/hneemann/Digital

Once "Digital" has been installed, the user will be able to download and interact with the various .dig simulation files.

# Lesson 1. LEDS and Switches.

This creates a simple LED and Switch interface which allows the user to enter binary data using "toggle" switches and display the data on an array of single LEDs and also in hexadecimal form using the 7-segment display component.

In addition to the LEDs and switches, the lesson introduces the 7474 dual flip-flop and the 74173 quad flipflop, which will be used throughout the series to provide a 4-bit register.

The 7474 is used to toggle the switch input between it's two states. Press once and the state of the output will change.

The 74173 illustrates the use of a quad flipflop being used as a storage register. It introduces the use of the Hold/Load input, Master Clear, Clock and tri-state control.

The LED and switch circuit simulation is reminiscent of the "Front Panels" from the minicomputers of the 1960s and the very early home computer kits of the early 1970s, which used toggle switches and indicator lamps to enter data into the machine and read back numerical results.

# Lesson 2 Program Counter and Memory

In this exercise I introduce the Program Counter and the concept of Memory addressing. 

The program counter is constructed from a pair of common 74xx163 4-bit counters that are cascaded together to create an 8-bit counter. This could be further extended easily to 12 or even 16 bits.

On the receipt of a positive going clock pulse, the counter increments its total by 1.

The counter has four outputs Q0,Q1,Q2 and Q3 which will count up the 4-bit binary sequence 0,1,2,3,4,5,6,7,8,9,10,11,12,,13,14,15. On reaching 15 the "ripple carry output" is asserted which is used to increment the next 4-bit stage.

Each counter has 4 parallel load inputs. By setting these and asserting the /LD input, the counter will be preset to a given count. The counter will then continue to count upwards from the given count.

This is the mechanism that allows a stored program to be executed and jump from one location to another.

# Lesson 3 Arithmetic and Logic Unit ALU

This lesson introduces the Arithmetic Logic unit or ALU, which is initially presented as a 4-bit building block.

This design has been adapted from a design by Dieter Muller - a TTL computer enthusiast.

It is based entirely on combinational logic, with the outputs being defined solely by the logic levels applied to the inputs.

It allows a 4-bit ALU slice to be constructed from just 5 common TTL ICs. It uses four 74xx153 multiplexers to create the logic unit and a 4-bit adder 74xx283 to provide addition and subtraction.

This makes a very economical ALU capable of AND, OR, XOR, NOT, ADD, SUB, INC, DEC and NEG using readily available TTL devices.

It could always be reduced to logic look up tables stored in a 16K ROM, but this solution is likely to be simpler, cheaper and faster.
 


