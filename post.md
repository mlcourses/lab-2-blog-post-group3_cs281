# Lab 2: Exploring Multiplexers and Adders in Digital Circuitry

## Overview and Motivation

In this week's lab, we are going to expand the introductory circuits, which we built in the last lab, with designing two important circuits. We will design and build a multiplexer and also design an adder circuit. There are four parts to the lab:

 1. Build a 2 to 1 mux out of AND, OR and NOT gates. Test with switches.
 2. Build a 4 to 1 mux using a 74150 mux chip. Test with switches.
 3. Build a 4 to 1 mux using a 74150 mux chip. Test with Arduino program.
 4. Design and build a 1 bit adder circuit.

Through this lab's experience, we aim to deepen our understanding of digital logic and its practical applications in computing.

## Materials

The materials we will be using in this lab are:
- PB-503 breadboard
- 74150 mux (16 to 1 mux)
- Wires
- Arduino kit
- IC data sheets
- Arduino controller with the USB adapter
- computer for the Arduino IDE
- 7404 chip (NOT gate)
- 7408 chip (AND gate)
- 7432 chip (OR gate)
- 7486 chip (XOR gate)


## Project Steps

In this project, we will follow four main steps. Initially, we will set up the breadboard, connecting a wire from the +5V supply to a top column pin and another from the ground to a top pin. 

**Safety First:** Before starting each step, we will power off the breadboard for safety, then turn it on to test our setup.

### Step 1 - Building a 2 to 1 mux using AND, OR, and NOT gates

Using the following circuit diagram: 

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/2%20to%201%20mux%20circuit.png" alt="alt text" width="550"/> 

We will build a 2 to 1 mux with just AND, OR, and NOT gates. As such, like our diagram, we will use two 7408 chips for the two AND gates, one 7404 inverter for the one NOT gate, and one 7432 chip for the one OR gate. For our inputs, we will use switch s5 for input line A and switch s6 for input line B. For the select line, we will use switch s1. The output will be connected to the logic probe (the LED light on the right of the breadboard).

And now we are ready to build our 2 to 1 mux:
- Put the chips accordingly like the circuit on the breadboard.
- Wire and ground the chips. Similar to the 7404 and 7408 chips we used in the previous lab, for the 7432 chip, the right hand corner is to be connected to Vcc or +5V and the lower left corner is to be connected to GND.
- The 7432 chip’s gates will also operate similarly to the 7408 chip, which means it has two inputs and onw output. The two inputs of this chip (gate 1A and gate 1B) will be connected to the output (gate 1Y) of the two 7408 chips. The output of the current pair of the 7432 chip (gate 1Y) will be connected to the logic probe.
- The first 7408 chip will be used to take in inputs from input line A and the output from the inverter. As such, gate 1A of the chip will be connected to switch s5 and gate 1B of the chip will be connected to the output of the 7404 inverter (gate 1Y). And as mentioned above, the output of this chip (gate 1Y) will be connected to the 7432 chip input gate 1A.
- The second 7408 chip will be used to take in inputs from input line B and the direct input from the selector. As such, gate 1A of the chip will be connected to switch s6 and gate 1B of the chip will be connected to switch s1. And as mentioned above, the output of this chip (gate 1Y) will be connected to the 7432 chip input gate 1B.
- For the 7404 inverter i.e. the NOT gate, pin 1 for the input gate 1A will be connected to switch s1, and once again as mentioned above, the output (gate 1Y) will be connected to the second input gate (gate 1B) of the first 7408 chip that is also taking input from input line A.

The final result should look something like this:







## Testing

## Conclusion




