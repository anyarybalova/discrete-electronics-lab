# 5-Bit Binary to Decimal Display (No Microcontrollers)

This is a simple hardware project that turns a 5-bit binary number into a decimal output using 74-series logic chips. It uses a basic binary-to-BCD conversion to drive three 7-segment displays—no microcontrollers, no firmware. 

Built mainly for fun and learning, it was a way to dive deeper into electronics and explore what can be made without relying on code. 

Its improving version of [`binary-to-decimal-display`](./binary-to-decimal-display). In this version it takes less components to build the same.  

## What This Does

- Takes a 5-bit binary input from DIP switch
- Using **74-series logic chips**
- Outputs the corresponding decimal number using 2 **7-segment displays** 

---


## Concept
The 1st digit is built exactly the same way as in [`binary-to-decimal-display`](./binary-to-decimal-display) which gives as the output 4 possible options, 00, 01, 10, 11.

To extract the **ones digit** (the second decimal digit) from a 5-bit binary number (e.g., extract `3` from `23`), the circuit subtracts a multiple of 10 — either `0`, `10`, `20`, or `30`. 
This subtraction removes the tens place, leaving only a result between `0–9`. That result is the digit to display.

---

## Components I Used
The same as [`binary-to-decimal-display`](./binary-to-decimal-display)

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

And adding new ones:
- 2 x Multiplexers - 74LS153
- 1 binary adder - 74LS83


## How It Works

1. A 2-bit selector chooses which value to subtract (0, 10, 20, or 30)
2. Each value is precomputed in two’s complement form and fed into a MUX
3. The selected complement is added to the **lower 4 bits** of the 5-bit input using a 74LS83 adder
4. The adder outputs the second decimal digit (range: 0–9)


For 5 bits substraction, would need 3 mux chips and 2 adder chips, but in this case, only the lower 4 bits (bits 0–3) of the 5-bit input are used. The most significant bit (bit 4) is ignored.

### Example

| Input (Binary) | Decimal | Selector | Subtract | Output (Digit) |
|----------------|---------|----------|----------|----------------|
| `10111`        | 23      | `10`     | 20       | `3`            |
| `11111`        | 31      | `11`     | 30       | `1`            |
| `00011`        | 3       | `00`     | 0        | `3`            |








