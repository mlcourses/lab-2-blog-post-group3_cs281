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

We will build a 2 to 1 mux with just AND, OR, and NOT gates. As such, like our diagram, we will use two 7408 chips for the two AND gates, one 7404 inverter for the one NOT gate, and one 7432 chip for the one OR gate. For our inputs, we will use switch `s5` for input line A and switch `s6` for input line B. For the select line, we will use switch `s1`. The output will be connected to the logic probe (the LED light on the right of the breadboard).

And now we are ready to build our 2 to 1 mux:
- Put the chips accordingly like the circuit on the breadboard.
- Wire and ground the chips. Similar to the 7404 and 7408 chips we used in the previous lab, for the 7432 chip, the right hand corner is to be connected to Vcc or +5V and the lower left corner is to be connected to GND.
- The 7432 chip’s gates will also operate similarly to the 7408 chip, which means it has two inputs and onw output. The two inputs of this chip (gate 1A and gate 1B) will be connected to the output (gate 1Y) of the two 7408 chips. The output of the current pair of the 7432 chip (gate 1Y) will be connected to the logic probe.
- The first 7408 chip will be used to take in inputs from input line A and the output from the inverter. As such, gate 1A of the chip will be connected to switch s5 and gate 1B of the chip will be connected to the output of the 7404 inverter (gate 1Y). And as mentioned above, the output of this chip (gate 1Y) will be connected to the 7432 chip input gate 1A.
- The second 7408 chip will be used to take in inputs from input line B and the direct input from the selector. As such, gate 1A of the chip will be connected to switch `s6` and gate 1B of the chip will be connected to switch `s1`. And as mentioned above, the output of this chip (gate 1Y) will be connected to the 7432 chip input gate 1B.
- For the 7404 inverter i.e. the NOT gate, pin 1 for the input gate 1A will be connected to switch `s1`, and once again as mentioned above, the output (gate 1Y) will be connected to the second input gate (gate 1B) of the first 7408 chip that is also taking input from input line A.

The final result should look something like this:


<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/2%20to%201.png" alt="alt text" width="450"/> 

### Step 2 - Designing a 4 to 1 mux using a 16 to 1 mux

Using the following 74150 mux i.e. a 16 to 1 mux:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/16%20to%201%20diagram.png" alt="alt text" width="550"/> 

We will design a 4 to 1 mux. We will use the lowest four data lines: `E0`, `E1`, `E2`, and `E3`. Accordingly, we will use switches `s8`, `s7`, `s6`, and `s5` for the data lines. For our two select lines, A and B, we will connect them to switches `s1` and `s2`. Once again, the output will be connected to the logic probe.

Now we are ready to design our 4 to 1 mux:
- Put the mux vertically on the breadboard.
- Wire and ground the chip. Similar to the chips we used in the previous step, the right hand corner (gate 24) is to be connected to Vcc or +5V and the lower left corner (gate 12) is to be connected to GND.
- Connect gates 5, 6, 7, and 8 to switches `s8`, `s7`, `s6`, and `s5` accordingly. These will be our four data lines.
- Connect gates 15, and 14 to switches `s1`, and `s2` accordingly. These will be our two select lines.
- Connect gate 10 to the logic probe. This will be our output.

Before moving forward, consult this function table:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/Function%20table.png" alt="alt text" width="550"/> 

From the function table, we notice that:
- In order for the mux to actually output from what is input from the data lines, we need to set the strobe to low. As such, connect the strobe - gate 9 to GND.
- For the other two select lines D and C, even if we are not using them, the mux would not know if we are using them or not. Because of that and the fact that we want to output from data lines `E0` to `E3`, we need to set the two select lines D and C to low. As such, connect gates 11 and 13 to GND.
- The output from the mux is inverted.
- To easier understand how the select lines are working, you can understand as if we are using the select lines to type out the binary for the number of the data line that we want the output to be from. For example, if A is Low (L) and B is High (H) or in the order of the function table, H - L, it will output from data line `E2`. 2 in binary is 10, and as such, High - Low.

The final result should look something like this:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/4%20to%201.png" alt="alt text" width="450"/> 

### Step 3 - Designing a 4 to 1 mux with Arduino

After you are done with the previous step, disconnect the wires to the 4 data lines, the 2 selectors (A and B only), and the output on the mux.

We will use the Arduino to test the operation of the mux. The Arduino will drive the inputs (data and control lines) for the mux, read the output of the mux, and run through a series of tests to verify the correct operation of the mux (and your circuit).

On the Arduino, connect the following pins accordingly to the mux:
- Pin 10 on the Arduino for data input A - data line `E0` on the mux
- Pin 11 on the Arduino for data input B - data line `E1` on the mux
- Pin 12 on the Arduino for data input C - data line `E2` on the mux
- Pin 13 on the Arduino for data input D - data line `E3` on the mux
- Pin 8 on the Arduino for select line 0 - select line `A` on the mux
- Pin 9 on the Arduino for select line 1 - select line `B` on the mux
- Pin 7 on the Arduino for output - output `w` on the mux
- GND on the Arduino (adjacent to pin 13) to GND on the breadboard

**Caution:** You will connect the GND pin on the data side, not on the power side of the Arduino to ground on the breadboard.

The final result should look something like this:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/4%20to%201%20mux%20with%20Arduino.png" alt="alt text" width="450"/> 

Write the following code: 

```c
const int S0[] = {0,0,1,1,0,0,1,1};
const int S1[] = {0,0,0,0,1,1,1,1};
const int A[] = {0,1,0,0,0,0,0,0};
const int B[] = {0,0,0,1,0,0,0,0};
const int C[] = {0,0,0,0,0,1,0,0};
const int D[] = {0,0,0,0,0,0,0,1};
// const int Y[] = {0,1,0,1,0,1,0,1};
// You are probably using a 74150, so the outputs are reversed.
// Use this Y instead:
const int Y[] = {1,0,1,0,1,0,1,0};
const int WAIT0 = 300;
const int WAIT1 = 2000;
int index = 0;
int x;  // for reading input
void setup() {
  // Serial Port setup for communication back to computer
  Serial.begin(9600);
  // data pins are outputs (for Arduino)
  pinMode(10,OUTPUT); // A
  pinMode(11,OUTPUT); // B
  pinMode(12,OUTPUT); // C
  pinMode(13,OUTPUT); // D
  // select pins are outputs (for Arduino)
  pinMode(8,OUTPUT);  // S0

pinMode(9,OUTPUT);  // S1
  // Mux output is input for Arduino
  pinMode(7,INPUT);
}
void loop() {
  // write data inputs to MUX
  digitalWrite(10,A[index]);
  digitalWrite(11,B[index]);
  digitalWrite(12,C[index]);
  digitalWrite(13,D[index]);
  // write select line inputs to MUX
  digitalWrite(8,S0[index]);
  digitalWrite(9,S1[index]);
  delay(WAIT0);   // give time for logic signal to propagate
  // read the MUX output
  x = digitalRead(7);
  // display the results
  Serial.print(index);
  Serial.print(" x:");
  Serial.print(x,BIN);
  Serial.print(", y:");
  Serial.print(Y[index],BIN);
  Serial.print("\t ");
  if ( x == Y[index] )
  {
    Serial.print(": OK\n");
  }
else {
    Serial.print(": BAD\n");
  }
  delay(WAIT1);
  index = (index+1) % 8;  // increment index
}
```
In the above code:
- The `const` arrays define inputs and selections for a 4-to-1 multiplexer experiment.
- `S0` and `S1` represent the selector inputs, deciding which data input (`A`, `B`, `C`, `D`) to pass through.
- `A`, `B`, `C`, `D` are data inputs, with each array representing one possible input state across different tests.
- `Y` shows the expected output for each combination of selector and data inputs, tailored for a 74150 mux chip where outputs are inverted.
- The values at corresponding indices across `S0`, `S1`, `A`, `B`, `C`, `D`, and `Y` together form a test case, demonstrating the mux's behavior under various input conditions.


As you write your code, remember to **choose the invert output Y** list as our outputs are reversed by using a 74150 mux (as noticed from the function table).

Run the program. You will have to open the “Serial Monitor” window in the Arduino IDE. This is the magnifying-glass like icon in the upper right corner of the IDE. You should see the results of your tests scroll across this window.

### Step 4 - Building the adder circuit using AND, OR, and XOR gates

Using the following circuit diagram: 

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/Adder%20circuit.png" alt="alt text" width="550"/> 

We will build the adder circuit with AND, OR, and XOR gates. As such, like our diagram, we will use two 7408 chips for the two AND gates, two 7486 chips for the two XOR gates, and one 7432 chip for the one OR gate. For our inputs, we will use switch `s1` for input A and switch `s2` for input B, and switch `s3` for `Cin`. The output will be connected to the logic probes (the LED light on the right of the breadboard).

And now we are ready to build our adder circuit:
- Put the chips accordingly like the circuit on the breadboard.
- Wire and ground the chips. Similar to the chips we used in the previous steps, for the  7486 chip, the right hand corner is to be connected to Vcc or +5V and the lower left corner is to be connected to GND
- Wire the switches `s1` and `s2` to the first pair of input of the first 7486 chip. The output of this chip will be connected to the first input of the second 7486 chip and the input of the bottom 7408 chip.
- Switches `s1` and `s2` will also be connected to the first pair of input of the top 7408 chip. The output of this 7408 chip will be connected to the first input of the 7432 chip.
- Connect switch `s3` to the second input of the second 7486 chip. This will be in the same pair of inputs with the output from the first 7486 chip. The output of the second 7486 chip will be connected to the 1st logic probe.
- Switch `s3` will also be connected to the second input of the bottom 7408 chip. This will be in the same pair of inputs with the output from the first 7486 chip. The output of this 7408 chip will be connected to the second input of the 7432 chip.
- The output of the 7432 chip will be connected to a logic probe.

The final result should look something like this:

<img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/one%20bit%20adder.png" alt="alt text" width="450"/> 

## Testing

- **For the first step:** After following the instructions for building a 2 to 1 mux using AND, OR, and NOT gates, we were happy to find out that the result was exactly what we expected. When `s1` (our selector), `s5`(A) and `s6`(B) were all low, the output was low. When `s1` and `s6` were low and `s5` was high, the output was high. When `s1` and `s5` were low and `s6` was high the output was high. When `s1` was high and both `s5` and `s6` were low, the output was low. Also, when `s1` and `s5` were high and `s6` was low, the output was low. Finally, in the two cases where `s1` and `s6` were high, the output was high regardless of what `s5` was.

    We can say that we found out that whenever `s1` is low, the output will be from input A, and whenever `s1` is high, the output will be from input B. 

    In boolean algebra it will be: `A¬S + BS`.

    [Testing our 2-1 mux](https://drive.google.com/file/d/1MBfiIWlyjF5bxTkZWnT7CRGPzY81Od0h/view?usp=sharing)

- **For the second step:** After following the instructions for designing a 4 to 1 mux using a 16 to 1 mux, we found out that the output we got, matched the truth table from step 2. For 4-1 mux, we have two selectors, and when the two selectors (`s1`,`s2` in the breadboard) are low, we are taking the input of E0 but inverting it (when `E0` is low, it will output high, and vice versa). When `s1` and `s2` are both high, the output is the invert of `E3`. When `s1` is low and `s2` is high, the output is the invert of `E1`. Lastly, when `s1` is high and `s2` is low, the output is the invert of `E2`. You can see all of these cases by clicking on the following link that will open our detailed video.

    [Testing our 4-1 mux](https://drive.google.com/file/d/1jmLiCxDXu9AMI3JJvbnmbXPTcvKItoSB/view?usp=sharing)

- **For the third step:** After following the instructions for using Arduino with the 4-1 mux, we verified the correctness of the 4-1 mux and out circuit. We got a proof for this correctness from our code as you can see in the following image:

    <img src="https://github.com/mlcourses/lab-2-blog-post-group3_cs281/blob/main/assets/Output%20of%204%20to%201%20Arduino.png" alt="alt text" width="450"/> 

    This program conducts a sequence of tests across various input and selector combinations, comparing the actual multiplexer output to predefined expected outcomes. It incorporates delays for signal stabilization and outputs test results on the serial monitor, indicating `OK` for matches and `BAD` for discrepancies.
    
- **For the fourth step:** After following the instructions of building an adder circuit, we found out that our boolean expression that we got from our truth table for adders, perfectly matched the output on the breadboard. The two boolean expressions we got are: 

    1. A ⊕ B ⊕ Cin
    2. AB + Cin(A ⊕ B)

    The gate that connects between these two expressions is OR.  Our result was according to these two boolean expressions. Whenever ONE of our inputs A, B or `Cin` (`s1`, `s2`, and `s3` accordingly) is high, the first boolean expression is correct and as a result the output on the breadboard is correctly high. When `s1` and `s2` are both high, the second expression is essentially correct and as a result the output in our breadboard was correctly high. Lastly, when `s3` (`Cin`) is true, and ONE of `s1` or `s2` are true, the second expression is essentially correct and the output on our breadboard was correctly high. In other cases where 0 or more than 1 input out of A,B, `Cin` were on, and either A\B and `Cin` were off, the output on our breadboard was low. This is exactly what we wanted to see as these boolean expressions representing the adder circuit and our result on the breadboard followed that pattern. Click on the following link to watch the video to see the correct result we got!

    [Testing our Adder](https://drive.google.com/file/d/1D4i9kRoaQVimo-0cT8rwiURQVD0VYMzu/view?usp=sharing)

## Conclusion

In this lab, we went through the basics of digital logic, building and testing multiplexers and adders. We started with simple 2-to-1 multiplexers and then moved to more complex 4-to-1 versions. We applied what we learned to real-life situations. The highlight was making a 1-bit adder, turning the ideas of Boolean algebra into something we could see and touch. This lab made us better understand digital logic and showed us how theory and practice can work together. Moving forward, the skills and knowledge we gained will help us tackle more complex topics in computing and electronics.



