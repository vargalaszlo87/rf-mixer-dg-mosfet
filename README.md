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

### Let's calc!

So, in this case the value of Rs is 470ohm. It would be good if the value of **Xc were 47ohm** on the given frequency. 

Xc = 1 / (2 * PI * f * C) from this: **C = 1 / (2 * PI * f * Xc)**

 - on the 300kHz: C = 11.2nF
 - on the 455kHz: C = 7.4nF
 - on the 800kHz: C = 4.2nF
 - on the 1MHz: C = 3.38nF
 - on the 2MHz: C = 1.69nF
 - on the 3MHz: C = 1.12nF
 - ...
 - on the 10MHz: C = 338pF

So, this circut is a tuned amplifier for 455kHz intermediate frequency, my **10nF** is a compromissed choice for IF. 🖤 **Yes**, i can also see 8.2nF were closer to calculated 7.4nF, but in practice **it's good to have a little reserve.**

### LC tank

The drain circuit contains an LC tank, acting as the load resistor, therefor this amplifier called **tuned amplifier** (with capacitive coupling). **What is the goal?** ❤️ Amplify at the given frequency (f0 of LC tank) and attenuate at the other frequency.

So this is a parallel LC circuit, and this is the formula:

<img width="150" height="44" alt="image" src="https://github.com/user-attachments/assets/beb8ffd4-24f7-46f2-979e-e31d14379a7a" />

We can now calculate: f0 = 1 / (2 * pi * sqrt(150e-6 * 820e-9) = 453.8kHz

⚠️ **Warrning!** ⚠️ **You cannot generate exactly 455kHz with these parameters, ca. 815.6pF were the good value.** ❤️ Thank God usually there is a large variaton in values, you can find such a capacitor that is close to 816pF. 

Of course, **the right solution** is a smaller capacitor and a parallel variable capacitor in this case. And **the best solution** is an IF transformer with adjustable value.

### Bandwidth

The LC tank has ohmic losses. According to manufacturer's specifications the capacitor has ca. 0.17ohm series resistance, the coil is 0.2ohm resistance in real.

Let's see what is the angular frequency at this frequency: 

<img width="110" height="37" alt="image" src="https://github.com/user-attachments/assets/fab48ce1-5305-4def-b4fe-db941b0b031b" />

w0 = 2 851 328 rad/s

Calc the Xl and Xc:

<img width="412" height="51" alt="image" src="https://github.com/user-attachments/assets/5af3b83a-fd13-45aa-a92c-a66ba464ac36" />

<img width="423" height="72" alt="image" src="https://github.com/user-attachments/assets/a4b7c784-3b3f-4b28-907d-2cbc77816b35" />

Losses of coil at the f0:

<img width="345" height="77" alt="image" src="https://github.com/user-attachments/assets/bd5f142b-a1d4-4b1e-b4ed-1ec57fddf457" />

Losses of capacitor at the f0:

<img width="350" height="70" alt="image" src="https://github.com/user-attachments/assets/2a81801a-d4ec-4867-af34-7db26939ef56" />

Total loss of the LC at the f0:

<img width="410" height="169" alt="image" src="https://github.com/user-attachments/assets/04bdabdf-b353-4568-b427-5e9cfea5cc6b" />

⚠️ **Warrning!** ⚠️ If you do not use a parallel resistor (R4), the bandwidth will be too narrow. Our goal is ca. 9kHz wide bandwidth.

The total resistance: 

<img width="356" height="175" alt="image" src="https://github.com/user-attachments/assets/46486cc6-0273-4496-9743-43fb35742573" />

The Q-factor:

<img width="276" height="176" alt="image" src="https://github.com/user-attachments/assets/15fa0564-918c-4894-acdc-8e03b1e858d8" />

And the Bandwidth:

<img width="326" height="82" alt="image" src="https://github.com/user-attachments/assets/b514d5e1-931d-4f5f-a4a8-d012ff720bb3" />




