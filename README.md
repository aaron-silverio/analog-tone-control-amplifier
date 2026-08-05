# Analog Tone Control and Karaoke Amplifier

## Overview
This project is a fully functional, custom-designed analog audio amplifier[cite: 1]. It processes standard left and right audio channels from a 3.5mm input, allowing the user to manipulate the signals through various analog stages[cite: 1].

## Features
* **Adjustable Tone Control:** Utilizes a Baxandall circuit for independent bass and treble adjustments[cite: 1].
* **Karaoke Mode:** Suppresses vocals by acting as a subtracting amplifier to subtract the left channel from the right[cite: 1].
* **Mixer Mode:** Acts as an inverting summing amplifier to combine the left and right audio channels[cite: 1].
* **Volume Display:** Features a 4-level LED ladder to visualize the output signal magnitude[cite: 1].

## Hardware and Tools
* **Components:** LF412CN Operational Amplifiers, potentiometers, capacitors, LEDs[cite: 1].
* **Software:** NI Multisim for circuit simulation and verification[cite: 1].

## Technical Challenges
* **Gain Management:** The initial stages could boost the signal by a factor of 20[cite: 1]. To prevent clipping, an attenuation block was designed with a gain of 1/20 using 2M Ohm and 100k Ohm resistors, bringing the output to a safe 0.5V to 1V threshold[cite: 1].
* **Hardware Rework:** After the initial PCB soldering, the final gain was incorrectly locked in[cite: 1]. This required physically cutting a resistor from the board and soldering a new one on the top layer to correct the gain stage without fabricating a completely new board[cite: 1].

## Hardware Implementation
Here is the final breadboard implementation of the circuit:

![Breadboard Implementation](images/breadboard_image_name.jpg)
*(Note: Replace the file name in the parentheses with your actual image file name)*

For a deep dive into the mathematical derivations, op-amp configurations, and simulation graphs for each block, please see the [Circuit Design Documentation](docs/circuit_design.md).