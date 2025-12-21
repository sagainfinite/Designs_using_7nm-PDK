## Tools and Models used for the following Simulations
1. **Ngspice**: Ngspice supports 7nm technology nodes through advanced FinFET models like BSIM-CMG (from UC Berkeley), enabling accurate simulations of nanoscale circuits. Ngspice DC sweep analysis for a logic inverter characterizes the voltage transfer curve (VTC), plotting output voltage versus swept input voltage to reveal gain, noise margins, and switching thresholds and so on.

2. **Xschem**: A schematic capture program primarily used for designing and simulating electronic circuits. It provides a graphical interface for drawing circuit schematics and integrates with various simulation tools, particularly SPICE simulators, to analyze circuit behavior.

3. **BSIM_CMG model** : BSIM-CMG, short for Berkeley Short-channel IGFET Model for Common Multi-Gate, serves as a compact simulation model for multi-gate transistors like FinFETs and nanowire FETs. Developed by UC Berkeley's Device Model Working Group (DMWG), it builds on classic BSIM models to capture intricate physics in these devices, including short-channel effects, quantum mechanics, and gate interactions. This model supports precise forecasting of device traits and circuit performance, making it a staple in industry and research for nanoscale IC design and refinement.
   A logical inverter uses a p-FET (pull-up) and n-FET (pull-down), both modeled with BSIM-CMG in a SPICE simulator, here I'll be using Ngspice.

