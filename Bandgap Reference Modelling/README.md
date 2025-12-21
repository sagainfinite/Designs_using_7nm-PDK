## Designing the Bandgap Reference Circuit

Self-Biased Cascode Current Mirror (SBCM) bandgap reference combines PTAT and CTAT voltages for temperature-stable Vref ~1.2V using FinFETs in 7nm process.

#### Following parameters to begin with:

Supply Voltage (DC) -> 1.75V <br>
Reference Resistance -> 50KΩ (ohms) <br>
Resistance near PTAT circuit -> 33KΩ (ohms) <br>
Temparature range -> -45°C to 125°C <br>
Output voltage -> 1.6V <br>
Runiq bias out 677 <br>


### Reference Schematic for the SBCM configuration:
![**Schematic for Reference**](https://github.com/sagainfinite/Designs_using_7nm-PDK/blob/main/Bandgap%20Reference%20Modelling/reference_img_for_bandgap.png) <br>

I begin with the **PTAT current generator**: Place a 33kΩ resistor **R1** between the drain of diode-connected NFETs **Q2** (gate-drain shorted), then connect identical NFETs **MN2** to ground. This creates the voltage difference across R1 that generates current rising linearly with temperature.

Next, construct the **self-biased cascode current mirror** using PFETs for high PSRR: **MP1** serves as diode-connected cascode (gate-drain shorted to net2), **MP2** mirrors current to the PTAT branch, and **MP6** biases the common gate (net2) for all PFET branches. This SBCM configuration ensures accurate current copying with high output impedance without external bias.

For the **CTAT voltage generator**, add diode-connected NFET and 50kΩ **R2** between Vref and Vctat. Vctat provides complementary-to-temperature behavior that decreases with rising temperature.

Implement the **voltage summing network** using PFET **MP3** (unit mirror from net2) connected to R2, producing temperature-stable ~1.2V output where the R2/R1 ratio scales the PTAT component to cancel CTAT slope.

Add **NFET cascode current sinks** for load matching: **MP3** as cascode, **MP4** diode-connected bias generator, and **MP5** reference sink, precisely matching PFET source currents.

**Signal flow**: PTAT (R1→voltage difference→SBCM→cascode sinks) + CTAT (Vctat via R2 divider) → Vref (~1.2V, zero tempco). The R2/R1 ratio and transistor matching determine temperature coefficient cancellation.

![**Xschem Schematic of Bandgap Reference**](https://github.com/sagainfinite/Designs_using_7nm-PDK/blob/main/Bandgap%20Reference%20Modelling/Xschem%20SS%20of%20BGR.png) <br>



## ACKNOWLEDGEMENT
To give thanks to Mr. Kunal Ghosh (Co-Founder of VSD) at [LinkedIn Profile](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/), RS Madhuri at [LinkedIn Profile](https://www.linkedin.com/in/royyurumadhuri/) and her [Git Repo for reference](https://github.com/vsdip/vsd-7nm/tree/main/Bandgap-Reference-Circuit-with-SCMB-with-ASAP-7nm-PDK-) as well as to the crew team at VSD!
