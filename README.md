# SIMULATION AND CHARACTERIZATION OF FINFET CIRCUITS USING ASAP7 PDK- 7nm TECHNOLOGY 
## NGSPICE
Ngspice stands as a **robust, open-source mixed-level/mixed-signal electronic circuit simulator**, rooted in the foundational SPICE3f5 developed at UC Berkeley. It excels at simulating analog and digital circuits across scales—from individual transistors to complete systems—making it indispensable for circuit design and verification in academia, industry, and hobbyist projects.

Key strengths include support for multiple analyses: **DC operating points, AC frequency responses, transient time-domain behaviors, noise characterizatio**n, and more. Its comprehensive device library covers diodes, BJTs, MOSFETs (including **advanced models like BSIM**), operational amplifiers, and passive components, enabling realistic modeling of everything from basic RC networks to sophisticated mixed-signal ICs.

A standout feature is its **seamless compatibility** with other SPICE tools, allowing direct import of netlists from HSPICE, LTSpice, or Spectre. Users can extend functionality through custom scripts, user-defined models, and plugins, tailoring it for specialized needs like emerging device technologies.

Common applications abound: engineers prototype analog filters or amplifiers virtually before hardware builds; educators teach circuit theory with hands-on simulations; researchers explore novel topologies, such as neuromorphic circuits or power electronics. Actively maintained by a global developer community, Ngspice receives regular updates, ensuring reliability and innovation. With its flexibility, zero cost, and cross-platform support, it democratizes advanced circuit simulation for all.
<br><br>
## XSCHEM
Xschem is an open-source schematic capture tool for **designing hierarchical analog/digital/mixed-signal circuits**, emphasizing speed and large-scale netlisting via a Tcl/Tk interface and C-based drawing engine.

#### Core Features
1. Hierarchical schematics with top-down design, supporting symbols, buses, vectors, and instance properties for complex systems.

2. Seamless Ngspice integration: generates SPICE netlists directly, runs simulations (DC, transient, AC), and back-annotates waveforms into schematics.

3. Library/symbol management, including generators for custom symbols and imports from GEDA/Lepton.

#### Usage Benefits
Edit visually, simulate via "Simulation" menu (e.g., batch Ngspice for inverters), view results inline. Ideal for **7nm PDK** flows like Sky130/**ASAP7 with BSIM-CMG**, enabling rapid prototyping without external tools.
<br><br>
## BSIM - CMG
BSIM-CMG, or Berkeley Short-channel IGFET Model for the Common Multi-Gate Structure, serves as a compact model for simulating multi-gate transistors such as FinFETs and nanowire FETs. Developed by the Device Model Working Group (DMWG) at UC Berkeley, it advances traditional BSIM models by accurately capturing complex physics like **short-channel effects, quantum mechanical effects, and gate coupling**. **Widely adopted in semiconductor industry and academia**, it enables precise prediction of device characteristics and performance for nanoscale integrated circuit design and optimization.

Using BSIM-CMG for Inverter Simulation
By renaming the .pm file to .sp as specified, you can employ the BSIM-CMG model for your inverter simulations. To access the latest FinFET models, visit the official site: https://www.bsim.berkeley.edu/models/bsimcmg/.

**Note:** Place the resulting .osdi files in the same working directory as your .sp file.
<br><br>

## Creating the schematic of the N-FET
Open the Xschem in terminal with the command ```xschem``` to launch the Xschem Environment. <br><br>
Use the shortcut: ```Shift + I``` to Insert symbol. <br><br>

**Choose Symbol window pops up** <br><br>
<img width="1084" height="957" alt="default setting for &#39;insert symbol&#39;" src="https://github.com/user-attachments/assets/60d8f6b2-e7ae-4987-9796-9edcfa7b0ee3" /><br><br>
Hit ```Current dir``` in the window pop-up and find the ASAP7 7nm folder repo for the symbol. 
<br><br><br>
**Select the nfet "asap_7nm_nfet.sym" required** <br><br>
<img width="1034" height="926" alt="find symbol in asap_7nm" src="https://github.com/user-attachments/assets/b14651a1-b2a4-4515-99ba-2abd4a5e08e3" />
<br><br><br>
**Xschem of nFET:**<br><br>
<img width="1062" height="820" alt="xschem of nfet char" src="https://github.com/user-attachments/assets/56a056db-2769-4283-8891-689cdef69795" />
<br><br><br>
**I<sub>D</sub> Graph for nFET** <br><br>
<img width="1419" height="641" alt="Id char for nfet" src="https://github.com/user-attachments/assets/1aa0e74c-683c-4d21-9292-a6b97a22851f" />
<br><br><br>
**I<sub>D</sub> vs V<sub>D</sub> Graph for nFET** <br><br>
<img width="1421" height="787" alt="Id vs Vd graph of nfet" src="https://github.com/user-attachments/assets/a6137e64-befa-43b8-94cf-9847f0f036c6" />
<br><br><br>
## ACKNOWLEDGEMENT
To give thanks to Mr. Kunal Ghosh (Co-Founder of VSD) at [LinkedIn Profile](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/), RS Madhuri at [LinkedIn Profile](https://www.linkedin.com/in/royyurumadhuri/) and her [Git Repo for reference](https://github.com/vsdip/vsd-7nm/tree/main) as well as to the crew team at VSD!
<br><br>
### References
[1] [SIMULATION AND CHARACTERISATION OF FINFET CIRCUITS USING ASAP - 7nm TECHNOLOGY [EDA - XSCHEM AND NGSPICE]](https://github.com/AsahiroKenpachi/asap_7nm_Xschem) <br>
[2] [Ngspice User’s Manual, Version 45 (ngspice release version)](https://ngspice.sourceforge.io/docs/ngspice-manual.pdf) <br>
[3] [Xschem Beginner's Guide](http://repo.hu/projects/xschem/xschem_man/xschem_man.html) <br>
[4] [NGSPICE: Open-Source Spice Simulator](https://ngspice.sourceforge.io/) <br>
