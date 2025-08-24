# 🚀 rf-mixer-dg-mosfet

This is a frequency mixer for AM radio with a dual-gate MOSFET. This is a well-know solution for pocket radios.

The dual-gate MOSFET acts as an RF multiplier. The RF signal is general fed to first Gate 1,  while the stronger Local Oscillator signal is fed to the second Gate 2. (By the way, you can also use this device to make AGC) This is a tuned common-source amplifier, with all its advantages and disadvantages.

## The circuit

<img width="679" height="666" alt="image" src="https://github.com/user-attachments/assets/6317e949-ca12-4302-aa47-a0267e6bb907" />

It's simple, but this circuit has good features:

- it's provides amplification
- bandwidth is 9kHz for AM receiving
- stable

## 🧭 Let's see how it works

The coupling capacitors (C1, C5) route the signals to the two gates. These values are good choices for more bands. 
