# 🚀 rf-mixer-dg-mosfet

This is a frequency mixer for AM radio with a dual-gate MOSFET. This is a well-know solution for pocket radios.

The dual-gate MOSFET acts as an RF multiplier. The RF signal is general fed to first Gate 1,  while the stronger Local Oscillator signal is fed to the second Gate 2. (By the way, you can also use this device to make AGC) This is a tuned common-source amplifier, with all its advantages and disadvantages.

## The circuit

<img width="711" height="687" alt="image" src="https://github.com/user-attachments/assets/856e7a13-110a-4c03-833a-be842db9d888" />

It's simple, but this circuit has good features:

- it's provides amplification
- bandwidth is 9kHz for AM receiving
- stable

## 🧭 Let's see how it works

The coupling capacitors (C1, C2) route the signals to the two gates. These values are good choices for more bands. What size gate resistor is the best? This question is not trivial. Choosing a higher value menas less load in the previous stage, but more sensitive to noise. If it is smaller, it is less sensitive to noise, but the load is greater. In this case the value 100k (R1, R2) is a good compromise, many factory circuits use it. (*by the way, these input "networks" (C1, R1 and C2, R2) are highpass filters,  **indeed!** T filters with Cgs1 and Cgs2, but it isn't important in this case*)

The network of source includes a resistor and a capacitor. In this case the resistor is a tool for biasing of MOSFET (it's also called **source degeneration**, further information can be found at the following link: [ECE 255, MOSFET Basic
Configurations](https://engineering.purdue.edu/wcchew/ece255s18/ece%20255%20s18%20latex%20pdf%20files/ece255Lecture_16_Mar8_MOSFET_Basic_Config.pdf)) The C3 is a bypass capacitor, AC acts as a short circuit (makes higher gain). **That's a good guestion, which bypass-capacitor size is the right one?** What is our goal? Our goal: **At a given frequency, Xc should bypass Rs!** It's a practival formula: **Xc <= Rs / 10** 

**Let's calc!**

So, in this case the value of Rs is 470ohm. It would be good if the value of Xc were 47ohm on the given frequency. 

Xc = 1 / (2 * PI * f * C) from this: **C = 1 / (2 * PI * f * Xc)**

 - on the 1MHz: C = 1 / (2 * PI * 1e6 * 47) = 3.38nF
 - on the 2MHz: C = 1,69nF
 - on the 3MHz: C = 1,12nF
 - ...
 - on the 10MHz: C = 338pF

So, my **1nF** is a compromissed choice for MF and lower HF band.




