# Analog Tone Control and Karaoke Amplifier

## Overview
This project is a fully functional, custom-designed analog audio amplifier. It processes standard left and right audio channels from a 3.5mm input, allowing the user to manipulate the signals through various analog stages.

<img width="564" height="752" alt="image" src="https://github.com/user-attachments/assets/778b8a1e-9b7f-4e17-a1a7-bcba24b96ae2" />

## Features
* **Adjustable Tone Control:** Utilizes a Baxandall circuit for independent bass and treble adjustments.
* **Karaoke Mode:** Suppresses vocals by acting as a subtracting amplifier to subtract the left channel from the right.
* **Mixer Mode:** Acts as an inverting summing amplifier to combine the left and right audio channels.
* **Volume Display:** Features a 4-level LED ladder to visualize the output signal magnitude.

## Hardware and Tools
* **Components:** LF412CN Operational Amplifiers, potentiometers, capacitors, LEDs.
* **Software:** NI Multisim for circuit simulation and verification.

## Technical Challenges
* **Gain Management:** The initial stages could boost the signal by a factor of 20. To prevent clipping, an attenuation block was designed with a gain of 1/20 using 2M Ohm and 100k Ohm resistors, bringing the output to a safe 0.5V to 1V threshold.
* **Hardware Rework:** After the initial PCB soldering, the final gain was incorrectly locked in. This required physically cutting a resistor from the board and soldering a new one on the top layer to correct the gain stage without fabricating a completely new board.

## Hardware Implementation
Here is the final breadboard implementation of the circuit alongside the annotated schematic:

<img width="702" height="525" alt="image" src="https://github.com/user-attachments/assets/17e53a6c-ac1b-490f-82eb-ec923774d0f4" />

<img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/26ac63a5-9577-4948-82d6-836b7086ef62" />


For a deep dive into the mathematical derivations, op-amp configurations, and simulation graphs for each block, please see the [Circuit Design Documentation](docs/circuit_design.md).
