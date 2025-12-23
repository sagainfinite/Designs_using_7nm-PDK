## Tools and Models used for the following Simulations
1. **Vitual Box** (Ubuntu: Bionic Beaver) for Windows: A VirtualBox Ubuntu Bionic Beaver setup refers to running Ubuntu 18.04 LTS (codename "Bionic Beaver") as a guest operating system inside Oracle VirtualBox virtualization software. This suits testing, development, or learning Linux in an isolated environment without dual-booting on the host devices/PCs. It's lightweight, with minimal resource needs for basic tasks like web browsing or coding.

2. **Ngspice**: Ngspice supports 7nm technology nodes through advanced FinFET models like BSIM-CMG (from UC Berkeley), enabling accurate simulations of nanoscale circuits. Ngspice DC sweep analysis for a logic inverter characterizes the voltage transfer curve (VTC), plotting output voltage versus swept input voltage to reveal gain, noise margins, and switching thresholds and so on.

3. **Xschem**: A schematic capture program primarily used for designing and simulating electronic circuits. It provides a graphical interface for drawing circuit schematics and integrates with various simulation tools, particularly SPICE simulators, to analyze circuit behavior.

4. **BSIM_CMG model** : BSIM-CMG, short for Berkeley Short-channel IGFET Model for Common Multi-Gate, serves as a compact simulation model for multi-gate transistors like FinFETs and nanowire FETs. Developed by UC Berkeley's Device Model Working Group (DMWG), it builds on classic BSIM models to capture intricate physics in these devices, including short-channel effects, quantum mechanics, and gate interactions. This model supports precise forecasting of device traits and circuit performance, making it a staple in industry and research for nanoscale IC design and refinement.
   A logical inverter uses a p-FET (pull-up) and n-FET (pull-down), both modeled with BSIM-CMG in a SPICE simulator, here I'll be using Ngspice.

5. **ASAP7 7nm PDK** : ASAP7 is a predictive process design kit (PDK) for 7nm FinFET technology, developed by Arizona State University (ASU) in collaboration with ARM for academic and research use. It models realistic assumptions for 7nm nodes, including EUV lithography for key layers, without tying to any specific foundry.<br>
       **Key Features:** The PDK includes FinFET transistor models with four threshold voltage options, a 54nm contacted poly pitch, and 21nm gate length for low subthreshold slope and DIBL. It provides standard cell libraries in a 7.5-track architecture, design rules for FEOL, MOL, and BEOL, plus collateral for tools like Cadence Virtuoso and Synopsys flows.

<br><br>

### Reference
[1] [For updates on ASAP7 PDK versions](https://asap.asu.edu/) <br>
[2] [FinFET Structure(Pg. 55): UC Berkeley - Oxygen-insertion Technology for CMOS Performance Enhancement](https://escholarship.org/content/qt2d46r42j/qt2d46r42j.pdf?t=q6z2kq) <br>
