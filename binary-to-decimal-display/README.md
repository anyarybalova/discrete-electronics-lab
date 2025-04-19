# 5-Bit Binary to Decimal Display (No Microcontrollers)

This is a simple hardware project that turns a 5-bit binary number into a decimal output using 74-series logic chips. It uses a basic binary-to-BCD conversion to drive three 7-segment displays—no microcontrollers, no firmware, just plain old logic gates. 

Built mainly for fun and learning, it was a way to dive deeper into electronics and explore what can be made without relying on code. 

It was surprisingly fascinating to implement what seemed like a "simple" algorithm entirely in hardware.


## What This Does

- Takes a 5-bit binary input from DIP switch
- Using **74-series logic chips**
- Outputs the corresponding decimal number using 2 **7-segment displays** 

---

## Why I Built It

I wanted to:
- Practice using logic gates and 74-series chips
- Avoid relying on microcontrollers or pre-programmed solutions
- Build something tangible and satisfying just using logic and a battery

---

## Components I Used

- 74-series logic chips
- 2 x 7-segment display drivers (like 74LS47)
- 2 x 7-segment displays 
- DIP switches (5 bits)
- Breadboard and jumper wires
- Battery 9V and allegators clips
- Optional: LEDs and Multimeter for debug and testing

---

## How It Works
 Based on the 5-bit input from the DIP switch, the circuit uses logic gates to generate two outputs:s:
  - 2-bit output for the **tens** place. This goes into a small logic circuit that converts it into BCD and sends it to a 7-segment display
  - 4-bit output for the **units** place, which is connected to a 74LS47 BCD-to-7-segment driver and another display.

---

## Steps

### 1. Connect power adapter  
Make sure your logic chips and displays are powered correctly.

### 2. Connect 5-bit DIP switch  
This will act as your binary input (values from 0 to 31).

### 3. Connect BCD logic and 7-segment displays  
Wire the tens and units outputs to their respective display drivers and 7-segment displays.

## 📬 Reach Out

If you're building something similar feel free to reach out. 

---

Thanks for checking out my little project!

