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

 


