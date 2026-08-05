# Circuit Design and Mathematical Derivations

This document breaks down the individual blocks of the amplifier, including the theory of operation, mathematical derivations, and simulation verification.

## Block 1: Mixer and Karaoke Modes
This block uses an LF412CN op-amp and a single-pole, dual-throw switch to toggle between two modes.

<img width="863" height="557" alt="image" src="https://github.com/user-attachments/assets/5dd5b763-debc-46b7-990e-951d1ada4ec2" />


**Mixer Mode (Inverting Summing Amplifier):**
$V_{out} = -(V_L + V_R)$
The feedback and input resistors are all set to 7.5k Ohms to ensure a gain of 1.

**Karaoke Mode (Subtracting Amplifier):**
$V_{out} = V_L - V_R$
By routing the left signal to the non-inverting input via a voltage divider and the right signal to the inverting input, the common vocal frequencies are subtracted and suppressed.

**Simulation Results:**
<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/55d3ab45-e96e-486f-82bf-446a552bd172" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/b556e9d5-ebc1-458f-8ff3-c572c14460b1" />


## Block 2: Baxandall Tone Control
This block allows independent control of bass and treble using 100k Ohm potentiometers and capacitors (47nF for bass, 100pF for treble).

<img width="796" height="599" alt="image" src="https://github.com/user-attachments/assets/2a2828c6-4df8-40f6-81ca-c57323602da6" />


The minimum and maximum gains are defined by:
$A_{min} = \frac{R}{R_{pot} + R}$
$A_{max} = \frac{R_{pot} + R}{R}$

To achieve a max gain of 10, the fixed resistors were calculated as 11.1k Ohms.

**Simulation Results:**
<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/ff930767-b278-466f-8fbb-6767250dbf20" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/04f7cc86-4e69-44d4-8c51-6cb34235e553" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/5648108a-933b-4439-aaf4-298e3b80847b" />


## Block 3: Volume Control
A 100k Ohm potentiometer acts as a simple voltage divider to scale the amplitude from 0% to 100%.

<img width="416" height="376" alt="image" src="https://github.com/user-attachments/assets/f1e381d3-a6f1-4919-a7f2-e7d6c9dd5a05" />


$V_{out} = V_{in} \cdot x$ (where x is the wiper fraction)

**Simulation Results:**
<img width="923" height="460" alt="image" src="https://github.com/user-attachments/assets/f616c766-8aa1-45d1-8bb7-6d07f3a881b1" />


## Block 4: Volume Display
A 4-level voltage ladder provides reference voltages (1.5V, 1.0V, 0.5V, 0.25V) to four op-amps acting as comparators.

<img width="498" height="552" alt="image" src="https://github.com/user-attachments/assets/23a67f4c-d1c9-4f15-8dc4-43f148f83965" />


To safely drive the LEDs (3.3V turn-on at 10mA) from a 15V supply, limiting resistors were calculated:
$R_{limiting} = \frac{15V - 3.3V}{0.01A} = 1170 \Omega$

**Simulation Results:**
<img width="366" height="521" alt="image" src="https://github.com/user-attachments/assets/cd57ea06-54d7-44f7-9e15-4a1a429932eb" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/725cbf2f-5126-40ca-8fef-01cfe15cdad4" />


## Block 5: Attenuation Stage
To counter the maximum potential gain of 20 from Blocks 1 and 2, this inverting amplifier stage applies a 1/20 gain. 

<img width="393" height="550" alt="image" src="https://github.com/user-attachments/assets/2111bf98-de27-4ae0-a193-30b0f056f088" />


High resistance values (2M Ohm input, 100k Ohm feedback) were chosen specifically to prevent circuit loading.

**Simulation Results:**
<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/9548854f-40e9-4419-9c4f-193b3fb5066d" />
