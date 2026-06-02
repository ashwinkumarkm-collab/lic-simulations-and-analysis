# Comprehensive Analysis of the Inverting Adder (Summing Amplifier)

## 1. Introduction to the Circuit Configuration
The inverting adder (or summing amplifier) is a highly versatile variation of the standard inverting amplifier. Instead of amplifying a single input signal, it mathematically adds multiple input voltages together, amplifies the sum by a specific gain, and outputs the inverted result. 

In this specific LTSpice simulation, the circuit is designed as a 3-input inverting adder using a uA741 operational amplifier. The three input AC voltage sources (V4, V1, V3) are connected in parallel to the op-amp's inverting (-) terminal through their respective input resistors (R2, R3, R4, all set to 10 kOhm). A single feedback resistor (R1, also 10 kOhm) connects the output back to the inverting terminal. The non-inverting (+) terminal is tied directly to ground (0 Volts).

## 2. Theoretical Foundation: Current and Voltage Source Equivalence
To truly understand how this circuit adds signals together, we can look at the theoretical hand-drawn models provided in the analysis. These notes perfectly illustrate the relationship between voltage, current, and the op-amp's feedback loop.

The hand-drawn diagrams show the principle of Source Transformation (converting a Thevenin voltage source to a Norton current source). 
* When an input voltage (Vin) is applied through a series resistor (Rx), it behaves exactly like a current source (I_in) pushing current into the circuit, where I_in = Vin / Rx.
* Because the op-amp's non-inverting terminal is grounded, the inverting terminal becomes a "virtual ground" (0 Volts). 
* The notes show that this virtual ground acts like a wall. The input current (I_in) reaches this node, but because the op-amp has infinite internal input impedance, the current cannot flow inside the op-amp. It is forced entirely through the feedback resistor (R), creating a voltage drop across it. 
* Therefore, the output voltage is entirely dictated by the input current being forced through the feedback resistor: Vout = - (I_in * R).

## 3. The Principle of Superposition and Current Summation
The adder circuit simply expands on the concept shown in the theoretical notes by adding multiple input branches. Because the inverting node is held strictly at 0 Volts (virtual ground), each input branch is completely isolated from the others. They do not interfere with each other. 

Instead, each input voltage independently generates its own current flowing toward the virtual ground:
* Current from branch 1 (I1) = V4 / R2
* Current from branch 2 (I2) = V1 / R3
* Current from branch 3 (I3) = V3 / R4

According to Kirchhoff's Current Law (KCL), all these individual currents meet at the virtual ground node and simply add together to form one total current (I_total = I1 + I2 + I3). This massive combined current has nowhere else to go but through the feedback resistor (R1).

## 4. Mathematical Derivation
We can calculate the exact theoretical output of the circuit by mapping the combined current across the feedback resistor.

Vout = - (I_total * R1)
Vout = - (I1 + I2 + I3) * R1
Vout = - [ (V4 / R2) + (V1 / R3) + (V3 / R4) ] * R1

Because the designer cleverly chose to make all resistors exactly the same value (R1 = R2 = R3 = R4 = 10 kOhm), the formula simplifies drastically. The resistance values cancel each other out, giving the circuit a "gain of 1" for every single input.

The final simplified equation becomes a pure mathematical addition:
Vout = - (V4 + V1 + V3)

## 5. Simulation Results and Waveform Inference
Looking at the LTSpice transient analysis, we can verify the mathematical derivation. The circuit utilizes three input sine waves with the same frequency (1 kHz) but different peak amplitudes:
* Input 1 (V4, light blue) = 0.1 V peak
* Input 2 (V1, red) = 0.2 V peak
* Input 3 (V3, blue) = 0.3 V peak

According to our derived formula, the peak output voltage should be the inverted sum of these three peaks:
Vout (peak) = - (0.1 V + 0.2 V + 0.3 V)
Vout (peak) = - 0.6 V (or -600 mV)

Observing the simulated output waveform (dark blue line, Vouta), we can see that when the three input sine waves reach their positive peaks, the output wave perfectly hits exactly -600 mV. Furthermore, because the output is well within the +/- 15V saturation limits of the op-amp power supply, the summed sine wave is clean and completely free of distortion. This confirms the circuit is operating perfectly as a unity-gain inverting summer.



# Comprehensive Analysis of the Subtractor Circuit (Difference Amplifier)

## 1. Introduction to the Circuit Configuration
The subtractor circuit, also known as a difference amplifier, is a highly useful operational amplifier configuration that outputs a voltage proportional to the difference between two input signals. 

In this LTSpice simulation, the circuit utilizes a uA741 op-amp with signals applied to both input terminals simultaneously:
* **The Inverting Branch:** An input voltage (V3) is applied to the inverting (-) terminal through an input resistor (R5 = 10 kOhm). A feedback resistor (R1 = 20 kOhm) connects the output back to this terminal.
* **The Non-Inverting Branch:** A second input voltage (V1) is applied to the non-inverting (+) terminal through an input resistor (R3 = 10 kOhm). A grounding resistor (R2 = 20 kOhm) connects this terminal to ground, forming a voltage divider.

## 2. Theoretical Foundation: The Superposition Theorem
Because signals are applied to both input terminals at the same time, the easiest way to understand and derive the output of this circuit is by using the Superposition Theorem. This theorem states that in a linear circuit, we can analyze the effect of each voltage source independently (by turning the other one off/grounding it) and then add the results together.

**Step A: Analyzing the Inverting Input (Turning V1 Off)**
If we temporarily ground V1 (set it to 0V), the non-inverting terminal (+) is pulled to ground through resistors R3 and R2. Because no current flows into the op-amp, the voltage at the (+) terminal becomes 0V. The circuit now acts exactly like a standard Inverting Amplifier. 
* The output caused purely by V3 is: Vout_inv = - (R1 / R5) * V3

**Step B: Analyzing the Non-Inverting Input (Turning V3 Off)**
If we temporarily ground V3, the circuit acts like a standard Non-Inverting Amplifier, but with a voltage divider at the input. 
* First, the voltage divider reduces the signal reaching the (+) pin. The voltage at the non-inverting pin (V_plus) is: V_plus = V1 * [R2 / (R3 + R2)]
* Second, the op-amp amplifies this voltage by the standard non-inverting gain formula: Gain = 1 + (R1 / R5)
* The output caused purely by V1 is: Vout_noninv = V_plus * Gain

## 3. Mathematical Derivation
Now we can apply the actual resistor values from the schematic to our Superposition steps to find the final equation.
* R1 = 20 kOhm, R5 = 10 kOhm
* R2 = 20 kOhm, R3 = 10 kOhm

**Calculating the Inverting Output:**
Vout_inv = - (20k / 10k) * V3 
Vout_inv = - 2 * V3

**Calculating the Non-Inverting Output:**
V_plus = V1 * [20k / (10k + 20k)] = V1 * (20/30) = V1 * (2/3)
Gain = 1 + (20k / 10k) = 1 + 2 = 3
Vout_noninv = [V1 * (2/3)] * 3 
Vout_noninv = 2 * V1

**Combining for the Final Output (Total Vout):**
Vout = Vout_noninv + Vout_inv
Vout = (2 * V1) - (2 * V3)
Vout = 2 * (V1 - V3)

*Note on Resistor Matching:* This elegant formula only works because the designer perfectly matched the resistor ratios (R1/R5 = R2/R3 = 2). This balanced ratio ensures the circuit subtracts the signals accurately and provides a uniform differential gain of 2.

## 4. Simulation Results and Waveform Inference
Looking at the LTSpice transient analysis, we can verify the mathematical derivation. The circuit utilizes two input sine waves operating at the same frequency (1 kHz) but with different peak amplitudes:
* Non-Inverting Input (V1, light blue line) = 0.1 V peak
* Inverting Input (V3, red line) = 0.3 V peak

According to our derived formula, the output voltage should be the difference between these two inputs multiplied by 2:
Vout = 2 * (V1 - V3)
Vout = 2 * (0.1 V - 0.3 V)
Vout = 2 * (-0.2 V)
Vout = -0.4 V (or -400 mV)

Observing the simulated output waveform (dark blue line, Vouta), we can see exactly this behavior in action. When both input sine waves reach their positive peaks simultaneously, the output wave drops to exactly -400 mV. Conversely, when the inputs hit their negative peaks (-0.1 V and -0.3 V), the output swings to exactly +400 mV. The output is a clean, distortion-free sine wave that perfectly validates the theoretical mathematics of the difference amplifier.