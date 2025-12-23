### What we'll be measuring (with corresponding spice commands):
#### Voltage Transfer Characteristic (Curve) of the inverter
``` plot nfet_out nfet_in   //Y-axis vs X-axis for the VTC ```
#### Threshold voltage (when nFET's output = input)
Vth is when the input voltage equals the output voltage on the voltage transfer characteristic (VTC) curve, marking the switching point. This occurs in the transition region where both NFET and PFET transistors operate in saturation, with equal drain currents. (For symmetric CMOS designs, Vth ideally equals VDD/2.) <br>
Plot the inverter VTC from SPICE DC sweep, Vth is the intersection where Vout = Vin, typically found graphically. <br>
``` meas dc vth when nfet_out = nfet_in ```
#### Gain (Av) and Maximum Gain
Gain is the ratio of change in output voltage to that of the input voltage. <br>
``` let gain_av = abs(deriv(nfet_out))      //absolute value taken ```
``` meas dc max_gain max gain_av      //value of max. 'gain_av' assigned to 'max_gain' ``` <br>
#### Noise Margin (from the VTC plotted)
Tolerance of a circuit to noise before signal integrity dwindles or is compromised. There are two limits:
##### Noise Margin High (NMH): This defines how much noise can degrade a logic high signal before it fails.
``` NMH = VOH(min) - VIH(min) ``` where, 
* VOH(min) is the minimum output high voltage from the driving inverter.
* VIH(min) is the minimum input recognized as logic high by the receiving inverter. <br>
``` let gain_tar= max_gain*0.999 ```
``` meas dc vil find nfet_in when gain_av = gain_tar cross = 1    //
 ```
##### Noise Margin Low (NML): It quantifies noise tolerance for logic low signals.
``` NML = VIL(max) - VOL(max) ``` where,
* VIL(max) is the maximum input accepted as logic low.
* VOL(max) is the maximum output low voltage. <br>
``` ksjd
```
**Note:** 
1. Larger the noise margin ensures the circuit is more resistance to voltage fluctuations/noise, maintaining proper logic level detection.
2. Higher margins improve noise immunity but may reduce switching speed.

<br><br>
## Tools and Models used for the following Simulations
1. **Vitual Box** (Ubuntu: Bionic Beaver) for Windows: A VirtualBox Ubuntu Bionic Beaver setup refers to running Ubuntu 18.04 LTS (codename "Bionic Beaver") as a guest operating system inside Oracle VirtualBox virtualization software. This suits testing, development, or learning Linux in an isolated environment without dual-booting on the host devices/PCs. It's lightweight, with minimal resource needs for basic tasks like web browsing or coding.

2. **Ngspice**: Ngspice supports 7nm technology nodes through advanced FinFET models like BSIM-CMG (from UC Berkeley), enabling accurate simulations of nanoscale circuits. Ngspice DC sweep analysis for a logic inverter characterizes the voltage transfer curve (VTC), plotting output voltage versus swept input voltage to reveal gain, noise margins, and switching thresholds and so on.

3. **Xschem**: A schematic capture program primarily used for designing and simulating electronic circuits. It provides a graphical interface for drawing circuit schematics and integrates with various simulation tools, particularly SPICE simulators, to analyze circuit behavior.

4. **BSIM_CMG model** : BSIM-CMG, short for Berkeley Short-channel IGFET Model for Common Multi-Gate, serves as a compact simulation model for multi-gate transistors like FinFETs and nanowire FETs. Developed by UC Berkeley's Device Model Working Group (DMWG), it builds on classic BSIM models to capture intricate physics in these devices, including short-channel effects, quantum mechanics, and gate interactions. This model supports precise forecasting of device traits and circuit performance, making it a staple in industry and research for nanoscale IC design and refinement.
   A logical inverter uses a p-FET (pull-up) and n-FET (pull-down), both modeled with BSIM-CMG in a SPICE simulator, here I'll be using Ngspice.

5. **ASAP7 7nm PDK** : ASAP7 is a predictive process design kit (PDK) for 7nm FinFET technology, developed by Arizona State University (ASU) in collaboration with ARM for academic and research use. It models realistic assumptions for 7nm nodes, including EUV lithography for key layers, without tying to any specific foundry.<br>
       **Key Features:** The PDK includes FinFET transistor models with four threshold voltage options, a 54nm contacted poly pitch, and 21nm gate length for low subthreshold slope and DIBL. It provides standard cell libraries in a 7.5-track architecture, design rules for FEOL, MOL, and BEOL, plus collateral for tools like Cadence Virtuoso and Synopsys flows.

![Xschem of nFET](<img width="1062" height="820" alt="xschem of nfet char" src="https://github.com/user-attachments/assets/56a056db-2769-4283-8891-689cdef69795" />)

<br><br>

### Reference
[1] [For updates on ASAP7 PDK versions](https://asap.asu.edu/) <br>
[2] [FinFET Structure(Pg. 55): UC Berkeley - Oxygen-insertion Technology for CMOS Performance Enhancement](https://escholarship.org/content/qt2d46r42j/qt2d46r42j.pdf?t=q6z2kq) <br>
[3] [Noise Margin affecting Inverter performance](https://resources.pcb.cadence.com/blog/2020-does-noise-margin-in-a-cmos-inverter-affect-performance)
