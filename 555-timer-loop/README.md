
# 555 Timer Loop

This is a small project I wasn’t even sure I should add to this repo. It’s just two blinking LEDs triggered in a loop using 555 timers. Very basic. But… it actually helped me understand a lot—how timers behave, how triggering works, and as well, about resistor values, capacitor sizes, and adding a potentiometer.

## 🔧 Components Used

- 2x **555 Timer ICs**
- 2x **LEDs** 
- 2x **Buttons** (connected to the Timer pin 2, and GND)
- 2x **Electrolytic Capacitors** (I used 10µF, but tweak as needed)
- 4x **Capacitors** - (I used 3.3µF)
- Resistors 
- 2x **Potentiometer** (to manually change blink speed of one timer, I used 500K)
- Jumper wires and breadboards
- 9V battery + alligator clips

Here’s a closer look at one of the timers with a potentiometer attached:

![Closer View - Timer with Potentiometer](./img/555-pot-close.jpg)

## ⚙️ What It Does
- Pressing the button on **Timer A** triggers the first LED. When the capacitor and potentiometer reach the threshold level, **Timer A** will output a LOW signal.
- When **Timer B** receives the LOW signal, it outputs a HIGH signal, turning on the second LED until the threshold is met. After **Timer B** outputs a LOW signal, the process repeats with **Timer A** turning on again.


## 📋 Steps to Build the Circuit

### Step 1: Build the First Timer Circuit

Start by building a simple 555 timer circuit that will blink an LED when a button is pressed. Here are the pin connections for **Timer A**:

1. **Pin 1 (GND)**: Connect to ground.
2. **Pin 2 (TRIG)**: Connect to one terminal of pushbutton (the other terminal goes to ground). Also, connect a 10kΩ pull-down resistor between this pin and ground to avoid floating input.
3. **Pin 3 (OUT)**: Connect to the anode of the LED (the cathode of the LED goes to the resistor.
4. **Pin 4 (RESET)**: Connect to +9V to disable reset functionality.
5. **Pin 5 (CV)**: Connect small capacitor (0.01µF) to ground to filter noise.
6. **Pin 6 (THRS)**: Connect to Pin 7 and Capacitor. 
7. **Pin 7 (DISCH)**:  Connect to a resistor that leads to a potentiometer (used to control timing). The other end of the potentiometer connects to +9V.
8. **Pin 8 (VCC)**: Connect to +9V.

The resistor–potentiometer–capacitor combination between **Pins 7 and 6** (and to ground) sets the timing for how long the LED stays on. Start with a 10kΩ resistor and a 10µF capacitor for a basic blink rate.

### Step 2: Build the Second Timer Circuit
Repeat the same steps as in Step 1 to build **Timer B**. The configuration is identical, and the timing components can be the same or different depending on your desired blinking pattern.

### Step 3: Connect the Timers

- **Timer A's Pin 3 (OUT)** connects to **Timer B's Pin 2 (TRIG)** to send a trigger signal. Place a 0.1µF capacitor between them to debounce the signal.
- **Timer B's Pin 3 (OUT)** connects to **Timer A's Pin 2 (TRIG)** to send a trigger signal, with another 0.1µF capacitor in between.
  
When Timer A turns off, it triggers Timer B to turn on, and vice versa, creating a looping effect between the two LEDs.
