# SIMULATION AND CHARACTERIZATION OF FINFET CIRCUITS USING ASAP7 PDK- 7nm TECHNOLOGY 
## NGSPICE
Ngspice stands as a **robust, open-source mixed-level/mixed-signal electronic circuit simulator**, rooted in the foundational SPICE3f5 developed at UC Berkeley. It excels at simulating analog and digital circuits across scales—from individual transistors to complete systems—making it indispensable for circuit design and verification in academia, industry, and hobbyist projects.

Key strengths include support for multiple analyses: **DC operating points, AC frequency responses, transient time-domain behaviors, noise characterizatio**n, and more. Its comprehensive device library covers diodes, BJTs, MOSFETs (including **advanced models like BSIM**), operational amplifiers, and passive components, enabling realistic modeling of everything from basic RC networks to sophisticated mixed-signal ICs.

A standout feature is its **seamless compatibility** with other SPICE tools, allowing direct import of netlists from HSPICE, LTSpice, or Spectre. Users can extend functionality through custom scripts, user-defined models, and plugins, tailoring it for specialized needs like emerging device technologies.

Common applications abound: engineers prototype analog filters or amplifiers virtually before hardware builds; educators teach circuit theory with hands-on simulations; researchers explore novel topologies, such as neuromorphic circuits or power electronics. Actively maintained by a global developer community, Ngspice receives regular updates, ensuring reliability and innovation. With its flexibility, zero cost, and cross-platform support, it democratizes advanced circuit simulation for all.

## XSCHEM
Xschem is an open-source schematic capture tool for **designing hierarchical analog/digital/mixed-signal circuits**, emphasizing speed and large-scale netlisting via a Tcl/Tk interface and C-based drawing engine.

#### Core Features
1. Hierarchical schematics with top-down design, supporting symbols, buses, vectors, and instance properties for complex systems.

2. Seamless Ngspice integration: generates SPICE netlists directly, runs simulations (DC, transient, AC), and back-annotates waveforms into schematics.

3. Library/symbol management, including generators for custom symbols and imports from GEDA/Lepton.

#### Usage Benefits
Edit visually, simulate via "Simulation" menu (e.g., batch Ngspice for inverters), view results inline. Ideal for **7nm PDK** flows like Sky130/**ASAP7 with BSIM-CMG**, enabling rapid prototyping without external tools.

## BSIM - CMG
BSIM-CMG, or Berkeley Short-channel IGFET Model for the Common Multi-Gate Structure, serves as a compact model for simulating multi-gate transistors such as FinFETs and nanowire FETs. Developed by the Device Model Working Group (DMWG) at UC Berkeley, it advances traditional BSIM models by accurately capturing complex physics like **short-channel effects, quantum mechanical effects, and gate coupling**. **Widely adopted in semiconductor industry and academia**, it enables precise prediction of device characteristics and performance for nanoscale integrated circuit design and optimization.

Using BSIM-CMG for Inverter Simulation
By renaming the .pm file to .sp as specified, you can employ the BSIM-CMG model for your inverter simulations. To access the latest FinFET models, visit the official site: https://www.bsim.berkeley.edu/models/bsimcmg/.

Note: These models use Verilog-A format (.va files), compiled via the OpenVAF compiler into .osdi files. Place the resulting .osdi files in the same working directory as your .sp file.

### References
[1] SIMULATION AND CHARACTERISATION OF FINFET CIRCUITS USING ASAP - 7nm TECHNOLOGY [EDA - XSCHEM AND NGSPICE]: https://github.com/AsahiroKenpachi/asap_7nm_Xschem
[2] Ngspice User’s Manual, Version 45 (ngspice release version): https://ngspice.sourceforge.io/docs/ngspice-manual.pdf
[3] Xschem Beginner's Guide: http://repo.hu/projects/xschem/xschem_man/xschem_man.html
