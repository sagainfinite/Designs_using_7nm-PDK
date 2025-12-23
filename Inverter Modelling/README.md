## Tools and Models used for the following Simulations
1. **Vitual Box** (Ubuntu: Bionic Beaver) for Windows: A VirtualBox Ubuntu Bionic Beaver setup refers to running Ubuntu 18.04 LTS (codename "Bionic Beaver") as a guest operating system inside Oracle VirtualBox virtualization software. This suits testing, development, or learning Linux in an isolated environment without dual-booting on the host devices/PCs. It's lightweight, with minimal resource needs for basic tasks like web browsing or coding.

2. **Ngspice**: Ngspice supports 7nm technology nodes through advanced FinFET models like BSIM-CMG (from UC Berkeley), enabling accurate simulations of nanoscale circuits. Ngspice DC sweep analysis for a logic inverter characterizes the voltage transfer curve (VTC), plotting output voltage versus swept input voltage to reveal gain, noise margins, and switching thresholds and so on.

3. **Xschem**: A schematic capture program primarily used for designing and simulating electronic circuits. It provides a graphical interface for drawing circuit schematics and integrates with various simulation tools, particularly SPICE simulators, to analyze circuit behavior.

4. **BSIM_CMG model** : BSIM-CMG, short for Berkeley Short-channel IGFET Model for Common Multi-Gate, serves as a compact simulation model for multi-gate transistors like FinFETs and nanowire FETs. Developed by UC Berkeley's Device Model Working Group (DMWG), it builds on classic BSIM models to capture intricate physics in these devices, including short-channel effects, quantum mechanics, and gate interactions. This model supports precise forecasting of device traits and circuit performance, making it a staple in industry and research for nanoscale IC design and refinement.
   A logical inverter uses a p-FET (pull-up) and n-FET (pull-down), both modeled with BSIM-CMG in a SPICE simulator, here I'll be using Ngspice.

5. **ASAP7 7nm PDK** : ASAP7 is a predictive process design kit (PDK) for 7nm FinFET technology, developed by Arizona State University (ASU) in collaboration with ARM for academic and research use. It models realistic assumptions for 7nm nodes, including EUV lithography for key layers, without tying to any specific foundry.<br>
       **Key Features:** The PDK includes FinFET transistor models with four threshold voltage options, a 54nm contacted poly pitch, and 21nm gate length for low subthreshold slope and DIBL. It provides standard cell libraries in a 7.5-track architecture, design rules for FEOL, MOL, and BEOL, plus collateral for tools like Cadence Virtuoso and Synopsys flows.
#### W/L Ratio
Has direct impact on the transistor's electrical properties:
* Drive Current (Id) capability
* Switching Speed
* Power Consumption

### Spice file creation and model used 
BSIM-CMG is a compact model for multi-gate MOSFETs, such as **FinFETs** and gate-all-around (GAA) transistors, developed by UC Berkeley for advanced nodes below 20nm. Used in PDKs like **ASAP7** for predictive 7nm design, it enables accurate circuit simulation of logic and memory blocks with scalability from device to system level. <br>
As I've used on the PC with Windows, I'll be using the Berkeley ' **bsimcmg.osdi** ', the alternate for the MAC users is ' bsimcmg_arch64.osdi '.
```
.control
pre_osdi /home/<user>/Desktop/asap_7nm_Xschem/bsimcmg.osdi
.endc
```
**The BSIM CMG model and its default values:**
<img width="828" height="721" alt="inverter_vtc s2 p5" src="https://github.com/user-attachments/assets/84617c59-5691-402d-b9f1-5b7e8e313fbd" /><br>
<img width="830" height="889" alt="inverter_vtc s2 p6" src="https://github.com/user-attachments/assets/fc02d656-c466-4374-abce-bed48a0552fd" />
<img width="821" height="808" alt="inverter_vtc s2 p7" src="https://github.com/user-attachments/assets/e60d9142-4989-4263-a33c-b855775887bc" />

### What we'll be measuring (with corresponding spice commands):
#### Voltage Transfer Characteristic (Curve) of the inverter
``` plot nfet_out nfet_in       // Y-axis vs X-axis for the VTC ```

**VTC Graph of the Inverter:**
<img width="1112" height="974" alt="nfet_in vs nfet_out graph of inveter_vtc" src="https://github.com/user-attachments/assets/09989884-7102-41aa-95fd-7597ba5d45ef" />

#### Switching Threshold Voltage (when nFET's output = input)
Vth is when the input voltage equals the output voltage on the voltage transfer characteristic (V<sub>TC</sub>) curve, marking the switching point. This occurs in the transition region where both NFET and PFET operate in saturation, with equal drain currents. <br>
**Note:** 
1. For symmetric CMOS designs, Vth (ideally) equals V<sub>DD</sub>/2.
2. To raise the V<sub>th</sub>, larger ratio is required, involves widening of the NFET
3. Similarly, to enhance the strenght of the NFET, will shift the Vth closer to ground, GND.
4. Use ```display``` command for getting the values of the active vectors.
<br>

Plot the inverter V<sub>TC</sub> from SPICE DC sweep, V<sub>th</sub> is the intersection where Vout = Vin, typically found graphically. <br>
```
meas dc vth when nfet_out = nfet_in
```
<br>
**Vth measured graphically:**
<img width="1117" height="1011" alt="Screenshot 2025-12-15 191811" src="https://github.com/user-attachments/assets/bb84ab20-68c3-438f-a8a3-06196c580981" />

#### Gain (Av) and Maximum Gain
Gain is the ratio of change in output voltage to that of the input voltage. <br>
``` 
let gain_av = abs(deriv(nfet_out))      // absolute value taken 
meas dc max_gain max gain_av      // value of max. 'gain_av' assigned to 'max_gain'
``` 
#### Noise Margin (from the V<sub>TC</sub> plotted)
Tolerance of a circuit to noise before signal integrity dwindles or is compromised. There are two limits (remember to check where it crosses over, decides the 'cross' value):
##### Noise Margin High (NMH): This defines how much noise can degrade a logic high signal before it fails.
``` NMH = VOH(min) - VIH(min) ``` where, 
* VOH(min) is the minimum output high voltage from the driving inverter.
* VIH(min) is the minimum input recognized as logic high by the receiving inverter. <br>
```
let gain_tar = max_gain * 0.999 
meas dc voh find nfet_out when gain_av = gain_tar cross = 1    // when nfet_out crosses gain for the 1st time
meas dc vih find nfet_in when gain_av = gain_tar cross = 2    // when nfet_in crosses gain for the 2nd time
let nmh = vih - voh                             // noise margin HIGH
 ```
##### Noise Margin Low (NML): It quantifies noise tolerance for logic low signals.
``` NML = VIL(max) - VOL(max) ``` where,
* VIL(max) is the maximum input accepted as logic low.
* VOL(max) is the maximum output low voltage. <br>
```
meas dc vil find nfet_in when gain_av = gain_tar cross = 1      // when nfet_in crosses gain for the 1st time
meas dc vol find nfet_out when gain_av = gain_tar cross = 2     // when nfet_out crosses gain for the 2nd time
let nml = vil - vol                               // noise margin LOW
print vth max_gain vil vol vih voh nml nmh        // print all the values to be displayed on the terminal
```
**Note:** 
1. Larger the noise margin ensures the circuit is more resistance to voltage fluctuations/noise, maintaining proper logic level detection.
2. Higher margins improve noise immunity but may reduce switching speed.

#### Transconductance, Gm
Ratio of the change in Drain current I<sub>D</sub> and change in V<sub>GS</sub>, Gate to Source voltage. In this case we know I<sub>D</sub> and V<sub>GS</sub> as equal to nfet_in. 
```
let id = v2#branch    // I<sub>D</sub>, drain current branch
let gm = real(deriv(id,nfet_in))
meas dc gm_max MAX gm     // check it in the graph for the gm_max peak
plot gm 
```
**The values of the parameters computed:**
<img width="1334" height="770" alt="the values of v_th and other parameters" src="https://github.com/user-attachments/assets/8ebae843-35f8-4eef-b1c4-327630050abc" />

#### Output Resistance, R<sub>out</sub>
Ration of output node voltage to cchnage in the Drain current, I<sub>D</sub>
```
let r_out = deriv(nfet_out,id)
plot r_out
plot id
```
**All the graphs for the Inverter:**
<img width="1919" height="976" alt="all the graphs of inverter_vtc2" src="https://github.com/user-attachments/assets/cf7b6ae1-cfc0-4d5a-9be3-5d8cf319cfe3" />

#### Propogation Delay, T<sub>p</sub>
The difference, in time, when output switches after the application of the input. (Calculated at 50% of input-output transition)<br>
Rise time, tr -> During transistion, output from 10% - 90% of maximum value <br>
Fall time, tf -> During transistion, output from 90% - 10% of maximum value <br>
(Some designs, also prefer the 30-70 split of the maximum value, depending on the designs)

Here, Transient Measurements from pulses given to 100 pico second of time
```
tran 0.1 100p
meas tran tpr when nfet_in = 0.35 rise = 1    // the 0.35 is in volts
meas tran tpf when nfet_out = 0.35 fall = 1
let tp = (tpr + tpf) / 2
```
#### Power Consumption
It is the product of integral of the transient current and the V<sub>DD</sub> divided by the time period.
```
let trans_current = v2#branch
meas tran id_pow integ trans_current from = 2e-11 to = 6e-11
let pwr = id_pow * 0.7                   // P=V.I where VDD is 0.7V here
let power = abs(pow/4e-11)
print tpr tpf tp id_pow pow power       // to display the following in the terminal
```
**Transient power and other computed values:**
<img width="1341" height="523" alt="transient power and other values" src="https://github.com/user-attachments/assets/6a27c3c4-5571-4b3d-905d-3578a25cf098" />
#### Frequency
The maximum signal frequency was calculated (using the delay time, previously calculated) <br>
   f = $\frac{1}{(tr+tp)}$  where, tr -> rise time and tf -> fall time
```
tran 0.1 100p                               //pulse given: <time_step> <total simulation time>
meas tran tr when nfet_in = 0.07 RISE = 1
meas tran tf when nfet_out = 0.63 FALL = 1
let t_delay = tr + tf
let f = 1/t_delay
print t_delay f
```
**With frequency and delay values:**
<img width="977" height="912" alt="transient analysis pt2 (with freq and rise and fall time)" src="https://github.com/user-attachments/assets/aa05ba72-489e-42a6-b4a0-b05fe1a348cb" />

<br><br>


<br><br>

### Reference
[1] [For updates on ASAP7 PDK versions](https://asap.asu.edu/) <br>
[2] [FinFET Structure(Pg. 55): UC Berkeley - Oxygen-insertion Technology for CMOS Performance Enhancement](https://escholarship.org/content/qt2d46r42j/qt2d46r42j.pdf?t=q6z2kq) <br>
[3] [Noise Margin affecting Inverter performance](https://resources.pcb.cadence.com/blog/2020-does-noise-margin-in-a-cmos-inverter-affect-performance)
