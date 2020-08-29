# Circuits Review

## Series DC Circuits

$$
R_T = R_1 + R_2 + R_3 ...
$$

Power follows the same form
$$
P_T = P_1 + P_2 + P_3 ...
$$
Where 
$$
P = VI = I^2R = \frac{V^2}{R}
$$
and we know that the current through resistors in series is the same. So if we sum R and solve for I we can the find the voltage drop across each resistor. 

**Kirchoff Voltage Law**: The sum of voltage rises around a closed path will always equal the sum of the voltage drops. 

## Parallel DC Circuits

$$
R_t = \frac{1}{1/R_1 + 1/R_2 + 1/R_3 ...}
$$

In parallel circuits, the voltage drop across each is the same, but the current splits. Meaning $I_t = I_1 + I_2$. 

**Kirchoff's Current Law**: The sum of currents entering a junction (or region) of a network must equal the sum of the currents leaving the same junction (or region).

## Superposition Theorem

The current through, or voltage across, any element of a network is equal to the algebraic sum of the currents of voltages produced independently by each source.

When removing a voltage source from a network schematic, replace it with a direct connection (short circuit) of zero ohms. Any internal resistances associated with the source must remain in the network. 

When removing a current source from a network schematic, replace it by an open circuit of infinite ohms. Any internal resistance associated with the source must remain in the network. 

##  The Basic Elements of Phasors

### Response of Basic R, L, and C Elements to a sinusoidal voltage or current

**Resistor**

Frequency gas no effect on the impedance
$$
I_m = \frac{V_m}{R}\\
V_m = I_m R
$$


**Inductor**

At a frequency of 0 Hz, an inductor takes on the characteristics of a short circuit. At very high frequencies, the characteristics of an inductor approach those of an open circuit.
$$
X_L = \omega L \\
X_L = \frac{V_m}{I_m}
$$
**Capacitor**

At or near 0 Hz, a capacitor takes on the characteristics of a short circuit. At very high frequencies, a capacitor takes on the characteristics of a sort circuit. 
$$
X_C = \frac{1}{\omega C}\\
X_C = \frac{V_m}{I_m}
$$










