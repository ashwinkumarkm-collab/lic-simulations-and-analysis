Comprehensive Analysis of the Inverting Amplifier
1. Introduction to the Circuit Configuration
The inverting amplifier is a fundamental operational amplifier circuit that outputs a signal that is exactly 180 degrees out of phase with its input. In this configuration, the input voltage signal (Vin) is applied to the inverting terminal (-) through an input resistor (Rin). The non-inverting terminal (+) is tied directly to the ground reference (0 Volts). A feedback resistor (Rf) connects the output terminal back to the inverting input terminal, establishing a negative feedback loop.

2. The Concept of Virtual Ground (Virtual Short)
To understand how this circuit operates, it is crucial to understand the concept of a "virtual ground" or "virtual short." An ideal operational amplifier has an open-loop voltage gain that is nearly infinite. The op-amp is designed to amplify the voltage difference between its two input terminals.

Because of the negative feedback loop provided by the feedback resistor (Rf), the op-amp will automatically adjust its output voltage to whatever level is necessary to keep the voltage difference between its two input terminals exactly at zero.

Since the non-inverting terminal (+) is physically connected to ground (0 Volts), the op-amp uses its output and the feedback loop to force the inverting terminal (-) to also be at 0 Volts. The two terminals are not physically shorted together by a wire, but they act as if they are. Therefore, the inverting terminal is called a "virtual ground." It sits at 0 Volts potential, but it cannot sink or source any current to the actual ground connection.

3. The Flow of Current
Another fundamental characteristic of an ideal op-amp is its infinite input impedance. This means that the internal resistance at the input pins is so high that absolutely zero current can flow into or out of the inverting (-) and non-inverting (+) terminals.

When the input voltage (Vin) is applied, it creates a potential difference across the input resistor (Rin). This causes an input current (I_in) to flow from the voltage source, through Rin, and toward the inverting terminal node.

When this current reaches the node at the inverting terminal, it faces a junction. However, because the op-amp itself has infinite input impedance, the current cannot enter the op-amp. It has only one path to take: it must flow entirely through the feedback resistor (Rf) toward the output terminal. Therefore, the current flowing through the input resistor is exactly equal to the current flowing through the feedback resistor.

4. Mathematical Derivation using Kirchhoff's Current Law (KCL)
We can prove the voltage gain of the amplifier by applying Kirchhoff's Current Law at the inverting node (let's call the voltage at this node V_minus).

KCL states that the algebraic sum of all currents entering and leaving a node must equal zero.
Current entering the node = Current leaving the node

Let the current through Rin be I_in.
Let the current through Rf be I_f.
Let the current entering the op-amp be I_opamp.