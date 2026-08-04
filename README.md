# Karaoke and Tone Control Audio Amplifier

<img width="564" height="752" alt="image" src="https://github.com/user-attachments/assets/6bff1176-8f27-4984-b12d-1881f7ff53b8" />

## Introduction
This project implements a fully functional audio amplifier that contains the ability to switch between a karaoke function or tone control, with additional aspects such as volume control and volume display. The circuit takes in the audio out from any audio source, such as a computer, through a 3.5mm audio jack and manipulates the signals of the left and right audio channels. The design was first implemented from scratch, drawing each functional block and manipulating voltage values through operational amplifiers. It was then tested on a breadboard and eventually soldered onto a custom Printed Circuit Board (PCB).

## Block 1: Mixer and Karaoke Mode
### Design Objective
This block takes the input of a 3.5 mm standard audio jack, represented by the left and right audio signal inputs. The design of this operational amplifier circuit utilizes a single pole, dual throw switch to allow the circuit to switch between mixer mode and karaoke mode. Mixer mode is an inverting summing amplifier that adds the two channels together, creating an output of $-(L + R)$. In karaoke mode, the operational amplifier acts as a subtracting amplifier that suppresses vocals by subtracting left from right $(L - R)$ to produce a karaoke effect.

<img width="863" height="557" alt="image" src="https://github.com/user-attachments/assets/7d1d6806-5f28-47e7-8c95-bc67d8126f1f" />


### Theory of Operation
The circuit routes the left and right audio channels through an operational amplifier based on the set mode. 

When the switch is in mixer mode, the left channel signal is routed to connect with the right channel so that both connect to the inverting terminal of the operational amplifier, with the noninverting input grounded. In this operation, the circuit acts as a summing inverting amplifier. It adds the two channels and produces a resulting output voltage of the inputs summed, times negative one.
Mixer mode: $$V_{out} = -(V_L + V_R)$$

In karaoke mode, the left signal gets routed to the noninverting input along with a voltage divider. The right signal connects to the inverting input as before. The whole circuit acts as a subtracting amplifier due to all the resistance values being the same.
Karaoke mode: $$V_{out} = V_L - V_R$$

### Derivations and Calculations
Starting with mixer mode, the circuit relies on the equation for an inverting summing amplifier:
$$V_{out} = -\left(\frac{R_f}{R_{iL}}V_L + \frac{R_f}{R_{iR}}V_R\right)$$

From this equation, the gain of the inputs is dependent on the value of the feedback resistor $R_f$ and the value of the input resistor for the corresponding input voltage amplitude. The left voltage input resistor is $R_{iL}$ and the right voltage input resistor is $R_{iR}$. Since the target output is $-(L+R)$, the feedback and input resistors are set to the same value to ensure a gain of one. 
$$V_{out} = -\left(\frac{R}{R}V_L + \frac{R}{R}V_R\right) = -(1V_L + 1V_R)$$
with $R = 7.5k\Omega$.

The resistor values were chosen to be $7.5k\Omega$ to ensure identical matching based on available 1% tolerance components.

For karaoke mode, the circuit switches the operational amplifier circuit to act as a subtracting amplifier. From the canonical difference amplifier equation:
$$V_{out} = V_L\left(\frac{R_g}{R_{iL} + R_g}\right)\left(1 + \frac{R_f}{R_{iR}}\right) - V_R\left(\frac{R_f}{R_{iR}}\right)$$

The gain for the left signal voltage is dictated by the voltage divider based on $R_g$ and the feedback plus the right signal input resistor. By setting these resistances equal ($R = 7.5k\Omega$), the entire equation can be simplified as:
$$V_{out} = V_L\left(\frac{R}{2R}\right)\left(1 + \frac{R}{R}\right) - V_R\left(\frac{R}{R}\right)$$

Canceling out all R values:
$$V_{out} = V_L - V_R$$

Therefore, in karaoke mode the amplitude of the left signal voltage gets subtracted by the amplitude of the right. In mixer mode, the amplitudes of both are added and the resulting output is the sum, times negative one.

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/9edc1b5f-3d1f-4e47-80a5-245c6560039d" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/e0ece06c-0777-4f1b-ae7c-1706813207ad" />


## Block 2: Tone Control
### Design Objective
This block takes the output from block one and allows the user to independently control the bass and treble frequencies of the audio signal with potentiometers. The resistor values ensure that the gain of this block is only within a range of 1/10 to 10 for both the bass and treble. This design is based on the Baxandall tone control circuit.

<img width="796" height="599" alt="image" src="https://github.com/user-attachments/assets/387bcd63-4b67-4825-9330-15c63d3cb67e" />


### Theory of Operation
Depending on the frequency of the input signal from block one, the operation of this circuit relies on the properties of capacitors. Designing for the same gain range for both bass and treble means that all primary resistors must be the same, except for the center $470k\Omega$ resistor.

At low frequencies, both capacitors act as open circuits. Since the 100pF capacitor is an open circuit, the bottom potentiometer has no effect on the circuit. At the same time, the 47nF capacitor acting as an open circuit forces the signal to travel through the top potentiometer. This gives the top potentiometer the ability to control the bass frequencies of the signal. 

At higher frequencies, the capacitors act as short circuits. When the 47nF capacitor shorts, the signal bypasses the top potentiometer. However, when the 100pF capacitor shorts, the bottom potentiometer connects with the inverting terminal of the operational amplifier. This makes the bottom potentiometer control higher frequencies, thereby controlling the treble.

At middle frequencies, the 47nF capacitor shorts, but the 100pF capacitor has a capacitance magnitude that makes it still act as an open circuit. The top potentiometer shorts, but the bottom potentiometer is also not connected. Neither potentiometer has control over the signal. The result is a unitary gain as the signal passes through the circuit.

### Derivations and Calculations
The equations for the minimum and maximum gains for both bass and treble of the Baxandall tone control circuit are:
$$A_{min} = \frac{R}{R_{pot} + R}$$
$$A_{max} = \frac{R_{pot} + R}{R}$$

The circuit uses $100k\Omega$ potentiometers. Solving for a max gain of 10: 
$$10 = \frac{100000 + R}{R}$$
$$10R = 100000 + R$$
$$9R = 100000$$
$$R \approx 11.1 k\Omega$$

With $R = 11.1k\Omega$, the max gain is 10. Because the minimum and maximum equations are inverses, this also gives the min gain of 1/10.

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/82836d62-a222-4e4e-81d3-532e73032b04" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/9dee6113-018c-4cd9-a22b-15bfb385f55a" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/a97d4251-457c-4e1b-852d-3f50c94f2ab7" />


## Block 3: Volume Control
### Design Objective
The purpose of this block is to allow the user to control the magnitude of the audio signal by using a potentiometer to adjust the voltage amplitude. This block takes the output of block 2 as its input and allows the signal to go from ground to its maximum level. 

<img width="416" height="376" alt="image" src="https://github.com/user-attachments/assets/3487e427-d907-4e99-9822-a62aa7463c41" />


### Theory of Operation
The amplitude of the audio signal gets put through a potentiometer that acts as a voltage divider. By adjusting the potentiometer, the output relies on the total percentage of the wiper that is not connected to ground. At 0%, the wiper is connected to ground, which mutes the output. At 100%, all of the signal from the input goes to the output, and at 50%, half of the signal goes to the output.

### Derivations and Calculations
This block relies on the voltage divider equation for a potentiometer:
$$V_{out} = V_{in} \left(\frac{x \cdot R_{pot}}{R_{pot}}\right)$$
where $x$ is the fraction of the wiper.

This simplifies to:
$$V_{out} = V_{in} \cdot x$$

Therefore, $x = 1$ means full volume, and $x = 0$ is mute.

<img width="923" height="460" alt="image" src="https://github.com/user-attachments/assets/44e3265b-dfc8-4801-a52d-169f7fc4e7de" />


## Block 4: Volume Display
### Design Objective
The objective of this block is to create a volume display using a 4-level voltage ladder with 4 LEDs. The input to this block is the output from block 3. The design uses operational amplifiers as comparators to light up LEDs when a certain voltage threshold is met. The four voltage reference levels are 1.5V, 1V, 0.5V, and 0.25V. To limit current through the LEDs, the circuit contains limiting resistors.

<img width="498" height="552" alt="image" src="https://github.com/user-attachments/assets/cd32922d-9b52-42e7-9ea3-d59554380496" />

### Theory of Operation
This block uses four operational amplifiers as comparators, where the input audio signal is routed to all non-inverting terminals. The inverting terminals of each are set to their corresponding voltage reference. The voltage ladder takes in the 15V supply and sets the needed voltage levels via voltage division. If the amplitude of the signal is greater than that of the set voltage reference, the operational amplifier saturates to 15V and the corresponding LED turns on.

### Derivations and Calculations
Because the current flowing through the series ladder is constant, resistance values are directly proportional to the voltage drops across them due to Ohm's law ($V = IR$). Taking the first resistor starting from the 15V power rail, it must drop the voltage to the needed reference of 1.5V:
$$15V - x = 1.5V$$
$$x = 13.5V$$

The rest of the voltage drops are as follows:
* Drop across R1: $15V - 1.5V = 13.5V$
* Drop across R2: $1.5V - 1.0V = 0.5V$
* Drop across R3: $1.0V - 0.5V = 0.5V$
* Drop across R4: $0.5V - 0.25V = 0.25V$
* Drop across R5: $0.25V - 0V = 0.25V$

By setting the common base resistor $R$ as $1k\Omega$, the resistances for the voltage ladder from top to bottom are $13.5k\Omega$, $500\Omega$, $500\Omega$, $250\Omega$, and $250\Omega$.

The comparators work by saturating to a positive voltage of 15V to turn on the LED. The formula for a limiting resistor is:
$$R_{limiting} = \frac{V_{out} - V_{turn\ on}}{I_{desired}}$$

The white LEDs used have a turn-on voltage of 3.3V, and the desired current is 10mA.
$$R_{limiting} = \frac{15V - 3.3V}{0.01A} = 1170\Omega$$

<img width="366" height="521" alt="image" src="https://github.com/user-attachments/assets/0fd1a716-7d28-474c-a2e4-285907e3df4a" />

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/8b91f34a-f98c-47f2-a4e6-c904862afb83" />


## Block 5: Output Buffer and Attenuation
### Design Objective
Because of the potential for the gains from blocks 1 and 2 to significantly boost the signal, this block serves to bring the audio level down to a safe line-level range. By making the gain less than one, the signal can fall within this threshold. To reduce loading, the circuit uses large resistance values in this block.

<img width="393" height="550" alt="image" src="https://github.com/user-attachments/assets/97979e7d-18cc-4b6d-8860-f658d7ab6ae8" />


### Theory of Operation
The gain from the operational amplifier reduces the amplitude of the voltage by a factor of 1/20. This is done through an inverting amplifier configuration, where the signal goes to the inverting terminal, and the noninverting terminal is grounded.

### Derivations and Calculations
The absolute greatest gain from block one is 2. Block two's determined max gain was 10. Therefore, an input signal can be boosted by 2 from block one, and then boosted by 10 by block two, resulting in a total max gain of 20. 

To curb this, this block uses an inverting amplifier with a gain less than one. From the inverting amplifier formula:
$$Gain = -\frac{R_f}{R_{in}}$$

By setting $R_f$ to a factor of 1 and $R_{in}$ to a factor of 20, the gain is 1/20. This results in a safe target max overall system gain of 1. The resistance values in this block must be significantly large enough to prevent loading. The resistance values are chosen to be $2M\Omega$ for the input resistor and $100k\Omega$ for the feedback resistor to achieve the 1/20 ratio.

<img width="975" height="486" alt="image" src="https://github.com/user-attachments/assets/72c053cc-fbaa-4eeb-9743-70b6edfa4e93" />

## Complete Circuit Implementation
The design progressed from theoretical block diagrams to software simulation, followed by physical breadboarding for verification, and finally permanent assembly on a Printed Circuit Board.

<img width="1018" height="697" alt="image" src="https://github.com/user-attachments/assets/e2ee339f-5b36-46d1-b7b2-b6340e6fa2a7" />

<img width="702" height="525" alt="image" src="https://github.com/user-attachments/assets/059e17f5-9ee2-45b9-9574-7a71d4074ec4" />

<img width="975" height="731" alt="image" src="https://github.com/user-attachments/assets/603c487c-547a-477b-bac7-7fabb73d8e8b" />

## Hardware Challenges and Conclusion
The project successfully transitioned a bottom-up circuit design into a fully functional hardware application. Manipulating audio signals to create vocal suppression and active tone adjustments demonstrated practical uses for operational amplifier configurations.

A significant challenge encountered during assembly involved an initial miscalculation of the final stage attenuation. The physical resistors were initially soldered for a 1/20 gain, but real-world testing indicated a 1/4 or 1/5 gain was more appropriate for the connected audio equipment. This required a physical rework of the board, demonstrating the importance of extensive real-world testing before finalizing a PCB layout. Despite this, the final board operates successfully, proving the viability of the theoretical design.
