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

- Practice using logic gates and 74-series chips
- Avoid relying on microcontrollers or pre-programmed solutions
- Build something tangible and satisfying just using logic and a battery

---

## Components I Used

- 74-series logic chips, I used only AND, OR and NOT
- Voltage Regulator LM7805
- 2 x 7-segment display decoder (like 74LS47)
- 2 x 7-segment displays
- DIP switches (5 bits)
- 2 Capacitors - 47µF, 0.1µF
- Resistors (see steps)
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

### 1. Connect Voltage regulator  

Before connecting anything else, it's important to make sure the voltage is right. Most 74-series chips require a stable 5V DC supply. If you're using a 9V battery (like I did), you'll need a voltage regulator to step it down to 5V, you risk burning out the chips.

I used an **LM7805** voltage regulator. Here's how to wire it:

- **Pin 1** → Input: connect to the 9V battery  
- **Pin 2** → Ground: connect to GND  
- **Pin 3** → Output: this will give you 5V

To stabilize the voltage I added two capacitors:
- A **47µF** capacitor between Pin 1 and GND  
- A **0.1µF** capacitor between Pin 3 and GND

After wiring it up, use a multimeter to check the output. It should read close to 5V before powering any of your logic chips.

> Note: If you're using a regulated bench power supply set to 5V, you can skip the voltage regulator.

<p>
  <img src="./img/voltage-step1-1.jpg" alt="Voltage Regulator" width="400" style="margin-right: 20px;">
  <img src="./img/voltage-step1-2.jpg" alt="Voltage Regulator multimeter" width="300">
</p>

### 2. Connect 5-bit DIP Switch

I'm not sure if standalone 5-bit DIP switches exist, so I used a combination of a 4-bit and a 1-bit switch. Each switch is wired as follows:

- One side of each switch is connected to **5V**  
- The other side is connected to the **input pins** of the logic circuit  
- Each input is also pulled down to **GND** using **15kΩ resistors**, to ensure a clear LOW state when the switch is off  
- Add jumper wires from each switch output and plug them into empty breadboard rows for now, or you can add the LEDs tempporary to test.

<img src="./img/DIP-swiitch-step2.jpg" alt="dip switch" width="300">
  
### 3. Connect BCD logic and 7-segment displays  

On a separate breadboard, connect the **74LS47** and the **7-segment display**. There are plenty of datasheets online for both components if you need pinouts.
Don’t forget to add **current-limiting resistors** for each segment of the display—values between **220Ω and 470Ω** work well, depending on brightness.

For testing, connect the **A, B, C, and D** inputs of the 74LS47 to either **GND or 5V** manually, and play around with different binary combinations. This is a good way to confirm that the correct numbers are being shown on the display before wiring it up to the rest of the logic circuit.

### 4. Wiring the First Digit (Tens Place)

Since I couldn’t figure out how to cleanly use a 2-digit 7-segment display (if you know how, feel free to DM me!), I went with a simple solution: use one display for the **tens** and another for the **units**.

Because the input is only 5 bits (values 0–31), the tens digit will only ever be 0, 1, 2, or 3. In binary, that means:

0000  
0001  
0010  
0011

So, the `D` and `C` inputs of the 74LS47 connected to the tens display will **always be 0**, and you can connect them directly to GND.

#### Logic for Input B (of 74LS47)

Looking at the binary values from 10 to 31:
from 10 to 31:
```
Dec   E D C B A
10    0 1 0 1 0
11    0 1 0 1 1
12    0 1 1 0 0
...
29    1 1 1 0 1
30    1 1 1 1 0
31    1 1 1 1 1
```
we can split the conditions for `B` into two main cases:

- From **10 to 15**: when `E = 0`, `D = 1`, and `B` or `C` is high  
- From **16 to 31**: when `E = 1`, and either `D = 0` or `B = 0`

That gives us the logic formula:

`B = (!E ∧ D ∧ (B ∨ C)) ∨ (E ∧ (!D ∨ !B))`

#### Logic for Input A (of 74LS47)

This one’s a bit more complex. The input `A` should be high in three ranges:

- From **10 to 15**: `E = 0`, `D = 1`, and `B` or `C` is high      => `!E ∧ D ∧ (B ∨ C)`
- From **16 to 19**: `E = 1`, `D = 0`, `C = 0`                     => `E ∧ !D ∧ !C`
- For **30 and 31**: `E = 1`, `D = 1`, `C = 1`, and `B = 1`        => `E ∧ D ∧ C ∧ B`

So the full logic expression is:

`A = (!E ∧ D ∧ (B ∨ C)) ∨ (E ∧ !D ∧ !C) ∨ (E ∧ D ∧ C ∧ B)`

#### Gate Usage & Layout

To build this with basic gates, I used:
- 2 AND gates  
- 1 OR gate  
- 1 NOT gate  

I placed some gates (like an AND and a NOT) in the middle of the board so they could be reused by the second digit logic later. The final OR gate was placed next to the 74LS47, since that’s where the result is fed into.


## 📬 Reach Out

If you're building something similar feel free to reach out. 

---

Thanks for checking out my little project!

