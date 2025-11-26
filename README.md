Half-Wave Voltage Doubler PCB (12 V AC → ~30 V DC)

This project implements a half-wave voltage doubler (Greinacher doubler) using two diodes and two electrolytic capacitors. The PCB is designed in EasyEDA and intended for a 12 V AC transformer input, producing approximately 30–32 V DC (no-load).

1. How the Circuit Works

The circuit uses two charging phases of the AC waveform:

Negative Half-Cycle:
- D1 conducts, D2 blocks.
- C1 charges up to the peak input voltage (Vp) minus one diode drop.
- This stored charge holds between cycles.

Positive Half-Cycle:
- D1 blocks, D2 conducts.
- The AC source and C1 voltage add in series.
- This higher voltage charges C2, resulting in nearly double the peak voltage.
- C2 holds the peak, forming a DC level close to twice Vp (minus diode losses).

2. Why the Input is 17 V in Simulation

Transformers are rated in RMS, but simulations use peak voltage.
For a 12 V AC transformer:

VRMS = 12 V
VP = VRMS × √2
VP = 12 × 1.414 ≈ 17 V

So in LTspice, the correct source is:

SINE(0 17 50)

(0 V offset, 17 V peak, 50 Hz frequency)

3. Expected Output Voltage

The ideal doubler output is:

VOUT ≈ 2VP - 2VD

Where:
- VP ≈ 17 V
- VD ≈ 0.7 V per diode (1N4007)

VOUT ≈ 2 × 17 - 2 × 0.7
VOUT ≈ 34 - 1.4 = 32.6 V (ideal)

Real hardware typically shows 30–32 V DC no-load.

4. Components Used

D1, D2 - 1N4007
C1 - 470 µF / 50 V
C2 - 470 µF / 50 V
Input Connector - 2-Pin Screw Terminal (AC)
Output Connector - 2-Pin Screw Terminal (DC)

5. Polarity & Orientation

Diodes:
- D1 anode → GND
- D1 cathode → C1/D2 junction
- D2 anode → C1/D1 junction
- D2 cathode → VOUT+

Capacitors:
- C1 (+) → C1/D2 junction
- C1 (–) → AC input
- C2 (+) → VOUT+
- C2 (–) → GND

6. PCB Design Notes

- 5.08 mm screw terminals
- Wide copper traces
- Clear silkscreen labels
- Through-hole components

7. Simulation Notes

LTspice transient analysis:
- Input: SINE(0 17 50)
- Duration: 0.2s
- Output settles around 30–32 V DC

8. Usage Notes

- Requires 12 V AC transformer (not DC)
- Output is unregulated
- Not for mains voltage
- Capacitors must be 50 V or higher

9. Applications

- Low-power high-voltage DC supply
- Educational demonstration
- Hobby electronics

