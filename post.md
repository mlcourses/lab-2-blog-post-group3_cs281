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


<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/2%20to%201.png" alt="alt text" width="450"/> 

### Step 2 - Designing a 4 to 1 mux using a 16 to 1 mux

Using the following 74150 mux i.e. a 16 to 1 mux:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/16%20to%201%20diagram.png" alt="alt text" width="550"/> 

We will design a 4 to 1 mux. We will use the lowest four data lines: E0, E1, E2, and E3. Accordingly, we will use switches s8, s7, s6, and s5 for the data lines. For our two select lines, A and B, we will connect them to switches s1 and s2. Once again, the output will be connected to the logic probe.

Now we are ready to design our 4 to 1 mux:
- Put the mux vertically on the breadboard.
- Wire and ground the chip. Similar to the chips we used in the previous step, the right hand corner (gate 24) is to be connected to Vcc or +5V and the lower left corner (gate 12) is to be connected to GND.
- Connect gates 5, 6, 7, and 8 to switches s8, s7, s6, and s5 accordingly. These will be our four data lines.
- Connect gates 15, and 14 to switches s1, and s2 accordingly. These will be our two select lines.
- Connect gate 10 to the logic probe. This will be our output.

Before moving forward, consult this function table:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/Function%20table.png" alt="alt text" width="550"/> 

From the function table, we notice that:
- In order for the mux to actually output from what is input from the data lines, we need to set the strobe to low. As such, connect the strobe - gate 9 to GND.
- For the other two select lines D and C, even if we are not using them, the mux would not know if we are using them or not. Because of that and the fact that we want to output from data lines E0 to E3, we need to set the two select lines D and C to low. As such, connect gates 11 and 13 to GND.
- The output from the mux is inverted.
- To easier understand how the select lines are working, you can understand as if we are using the select lines to type out the binary for the number of the data line that we want the output to be from. For example, if A is Low (L) and B is High (H) or in the order of the function table, H - L, it will output from data line E2. 2 in binary is 10, and as such, High - Low.

The final result should look something like this:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/4%20to%201.png" alt="alt text" width="450"/> 

### Step 3 - Designing a 4 to 1 mux with Arduino

After you are done with the previous step, disconnect the wires to the 4 data lines, the 2 selectors (A and B only), and the output on the mux.

We will use the Arduino to test the operation of the mux. The Arduino will drive the inputs (data and control lines) for the mux, read the output of the mux, and run through a series of tests to verify the correct operation of the mux (and your circuit).

On the Arduino, connect the following pins accordingly to the mux:
- Pin 10 on the Arduino for data input A - data line E0 on the mux
- Pin 11 on the Arduino for data input B - data line E1 on the mux
- Pin 12 on the Arduino for data input C - data line E2 on the mux
- Pin 13 on the Arduino for data input D - data line E3 on the mux
- Pin 8 on the Arduino for select line 0 - select line A on the mux
- Pin 9 on the Arduino for select line 1 - select line B on the mux
- Pin 7 on the Arduino for output - output w on the mux
- GND on the Arduino (adjacent to pin 13) to GND on the breadboard

**Caution:** You will connect the GND pin on the data side, not on the power side of the Arduino to ground on the breadboard.

The final result should look something like this:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/4%20to%201%20mux%20with%20Arduino.png" alt="alt text" width="450"/> 




## Testing

## Conclusion




