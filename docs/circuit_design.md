# Circuit Design and Mathematical Derivations

This document breaks down the individual blocks of the amplifier, including the theory of operation and mathematical derivations[cite: 1].

## Block 1: Mixer and Karaoke Modes
This block uses an LF412CN op-amp and a single-pole, dual-throw switch to toggle between two modes[cite: 1].

![Block 1 Schematic](../schematics/block1_schematic_name.png)

**Mixer Mode (Inverting Summing Amplifier):**
$V_{out} = -(V_L + V_R)$
The feedback and input resistors are all set to 7.5k Ohms to ensure a gain of 1[cite: 1].

**Karaoke Mode (Subtracting Amplifier):**
$V_{out} = V_L - V_R$
By routing the left signal to the non-inverting input via a voltage divider and the right signal to the inverting input, the common vocal frequencies are subtracted and suppressed[cite: 1].

## Block 2: Baxandall Tone Control
This block allows independent control of bass and treble using 100k Ohm potentiometers and capacitors (47nF for bass, 100pF for treble)[cite: 1].

![Block 2 Schematic](../schematics/block2_schematic_name.png)

The minimum and maximum gains are defined by:
$A_{min} = \frac{R}{R_{pot} + R}$
$A_{max} = \frac{R_{pot} + R}{R}$

To achieve a max gain of 10, the fixed resistors were calculated as 11.1k Ohms[cite: 1].

## Block 3: Volume Control
A 100k Ohm potentiometer acts as a simple voltage divider to scale the amplitude from 0% to 100%[cite: 1].

![Block 3 Schematic](../schematics/block3_schematic_name.png)

$V_{out} = V_{in} \cdot x$ (where x is the wiper fraction)

## Block 4: Volume Display
A 4-level voltage ladder provides reference voltages (1.5V, 1.0V, 0.5V, 0.25V) to four op-amps acting as comparators[cite: 1].

![Block 4 Schematic](../schematics/block4_schematic_name.png)

To safely drive the LEDs (3.3V turn-on at 10mA) from a 15V supply, limiting resistors were calculated[cite: 1]:
$R_{limiting} = \frac{15V - 3.3V}{0.01A} = 1170 \Omega$

## Block 5: Attenuation Stage
To counter the maximum potential gain of 20 from Blocks 1 and 2, this inverting amplifier stage applies a 1/20 gain[cite: 1]. 

![Block 5 Schematic](../schematics/block5_schematic_name.png)

High resistance values (2M Ohm input, 100k Ohm feedback) were chosen specifically to prevent circuit loading[cite: 1].