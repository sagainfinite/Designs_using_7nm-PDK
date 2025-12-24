## Designing the Bandgap Reference Circuit

Self-Biased Cascode Current Mirror (SBCM) bandgap reference combines PTAT and CTAT voltages for temperature-stable Vref ~1.2V using FinFETs in 7nm process.

#### Following parameters to begin with:

Supply Voltage (DC) -> 1.75V <br>
Reference Resistance -> 1KΩ <br>
Temparature range -> -45°C to 125°C <br>
Output voltage -> 1.6V <br>
Runiq (bias) -> 677Ω <br>


### Reference Schematic for the SBCM configuration:
![**Schematic for Reference**](https://github.com/sagainfinite/Designs_using_7nm-PDK/blob/main/Bandgap%20Reference%20Modelling/reference_img_for_bandgap.png) <br>

#### Step-wise Schematic creation
I begin with the **PTAT current generator**: Place a 33kΩ resistor **R1** between the drain of diode-connected NFETs **Q2** (gate-drain shorted), then connect identical NFETs **MN2** to ground. This creates the voltage difference across R1 that generates current rising linearly with temperature.

Next, construct the **self-biased cascode current mirror** using PFETs for high PSRR: **MP1** serves as diode-connected cascode (gate-drain shorted to net2), **MP2** mirrors current to the PTAT branch, and **MP6** biases the common gate (net2) for all PFET branches. This SBCM configuration ensures accurate current copying with high output impedance without external bias.

For the **CTAT voltage generator**, add diode-connected NFET and 50kΩ **R2** between Vref and Vctat. Vctat provides complementary-to-temperature behavior that decreases with rising temperature.

Implement the **voltage summing network** using PFET **MP3** (unit mirror from net2) connected to R2, producing temperature-stable ~1.2V output where the R2/R1 ratio scales the PTAT component to cancel CTAT slope.

Add **NFET cascode current sinks** for load matching: **MP3** as cascode, **MP4** diode-connected bias generator, and **MP5** reference sink, precisely matching PFET source currents.

**Signal flow**: PTAT (R1→voltage difference→SBCM→cascode sinks) + CTAT (Vctat via Runiq divider) → Vref (~1.2V, zero tempcoeff). The Runiq/R1 ratio and transistor matching determine temperature coefficient cancellation.

### Xschem Schematic of Bandgap Reference
<img width="1021" height="648" alt="BGR Schematic in Xschem" src="https://github.com/user-attachments/assets/8fe77e39-1dfe-4ee6-b3bb-dee8f33a2c32" />

### To compute the Vref at particular Temperatures and their startup time and the VDD variation/Line regulation

Change the VDD supply value for every trial with <br>
```V2 vdd GND 1.2V       // the VDD value which you want to trial with``` <br><br>
Now, running the dc sweep (Note: don’t run transient when running DC) <br>
```
.dc temp -45 150 5
.control
run
plot v(Vref)
plot v(Vctat)
let vptat = v(Vref) - v(Vctat)
plot vptat
let tc = deriv(v(Vref))/1.24        // Temperature Co-efficient
plot tc
print vref vptat vctat tc        //for all the values it runs at
``` 

### Here are the graphs obtained for a particular run 
<img width="1017" height="675" alt="Vref graph" src="https://github.com/user-attachments/assets/efc033dd-5f1b-4635-9294-953ed1acce53" /> <br>
<img width="858" height="666" alt="VCTAT Graph" src="https://github.com/user-attachments/assets/55d9b928-bb75-4bea-8cab-0d3e51693d9a" /> <br>
<img width="943" height="681" alt="VPTAT graph" src="https://github.com/user-attachments/assets/ad2d72e1-48a0-431a-ad8c-f8b00b233129" /> <br>
<img width="994" height="667" alt="Temperature Coefficient Graph" src="https://github.com/user-attachments/assets/a7825c15-02cb-4adc-b1d7-67d909f674bf" /> <br><br><br>
### Here are the values obtained for the temp sweeps over the graphs
<img width="905" height="875" alt="Temp sweep with vref, vctat, vptat" src="https://github.com/user-attachments/assets/1532b5a4-bba9-4157-80a1-d644225e3856" /> <br>
<img width="482" height="868" alt="Temp sweep with TC" src="https://github.com/user-attachments/assets/f1da673c-7916-45d3-92b9-c3ccd5414886" /> <br><br>

### For the computation of Line Regulation(in mV/V) and Start-up time (in ns)(graphically) 
```
meas dc Vref_max max v(Vref)
meas dc Vref_min min v(Vref)
* Line regulation (mV/V) (Note: don’t run dc when running transient)
let line = (((Vref_max-Vref_min)/(1.2-0.7))*1e3)
meas dc Line_Reg max line
```
<br>
<img width="1436" height="714" alt="line regulation of VDD" src="https://github.com/user-attachments/assets/154858d2-be89-48f8-a4b9-2dc5e18bbf28" /> <br> <br>
<img width="764" height="800" alt="startup time graphically" src="https://github.com/user-attachments/assets/0631b272-c098-4cb5-88d2-d14b809bf522" /> <br>
<br><br>

## ACKNOWLEDGEMENT
To give thanks to Mr. Kunal Ghosh (Co-Founder of VSD) at [LinkedIn Profile](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/), RS Madhuri at [LinkedIn Profile](https://www.linkedin.com/in/royyurumadhuri/) and her [Git Repo for reference](https://github.com/vsdip/vsd-7nm/tree/main/Bandgap-Reference-Circuit-with-SCMB-with-ASAP-7nm-PDK-) as well as to the crew team at VSD!

### References
[1] [Band Gap Reference Circuit (BGR)](https://github.com/vsdip/vsdopen2021_bgr)
