# Week 2 Task 2 
# 📘 VSDBabySOC Functional Modelling 

This is a compact SOC based on RISC-V architecture, this is a small-scale SOC with open-source intellectual property (IP) cores this is very useful for educational purpose. This BabySOC has 3 components a RISC-V processor (`rvmyth`), a PLL (Phase-Locked Loop) module (`pll`), and a DAC (Digital-to-Analog Converter) module (`dac`). This project demonstrates integration of these IP cores and aims to simulate and verify the design behavior using simulations.

--- 

## Project required folders 
- `src/include/` - Contains header files (`*.vh`) with necessary macros or parameter definitions.
- `src/module/` - Contains Verilog files for each module in the SoC design.
- `output/` - Directory where compiled outputs and simulation files will be generated.

## Tools 
- **Icarus Verilog** for compilation  
- **GTKWave** for viewing waveform files  
- **Sandpiper** for file convertion   
- Unix-like environment

---

## Design Modelling 

### 1. Install Python3 & Sandpiper
```txt
sudo apt install python3-venv python3-pip
python3 -m venv sp_env
source sp_env/bin/activate
pip install pyyaml click sandpiper-saas
```

### 2. Setup and Prepare Project Directory
Clone or set up the directory structure as follows:  
```txt 
git clone https://github.com/manili/VSDBabySoC/.git
```  
You should be seeing the folder structure as below:
```txt
VSDBabySoC/
├── src/
│   ├── include/
│   │   ├── sandpiper.vh
│   │   └── other header files...
│   ├── module/
│   │   ├── vsdbabysoc.v      # Top-level module integrating all components
│   │   ├── rvmyth.tlv          # RISC-V core module
│   │   ├── avsdpll.v         # PLL module
│   │   ├── avsddac.v         # DAC module
│   │   └── testbench.v       # Testbench for simulation
└── output/
```

### 3. Convert .tlv into .v 
This command converts rvmyth.tlv and rvmyth_gen.tlv codes into rvmyth.v and rvmyth_gen.v  
this is done as icarus verilog simulates only verilog files and not tlv file  
this genereated files will be saved into VSDBabySOC/src/module/ folder

```txt
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/sandpiper.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>


### 4. folder to save simualtion outptuts 
this will create a new empty folder in VSDBabySOC/
```txt
mkdir -p VSDBabySoC/output/pre_synth_sim
```

### 5. Compilation of verilog files
```txt
iverilog -o output/pre_synth_sim/pre_synth_sim.out \
  -DPRE_SYNTH_SIM \
  -I src/include -I src/module \
  src/module/testbench.v
```
> this will generate a '.out' file in output/pre_synth_sim/ 
```txt
./pre_synth_sim.out
```
> when this command is run it generates '.vcd' file used in gtkwave 
```txt
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/sim_commands.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## Waveform Analysis 
### 1. Full simulated Wave 
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/full_sim_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

### 2. Reset operation 
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/dataflow_in_modules.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>  

> When the reset signal is high (logic 1), internal signals such as RV_TO_DAC show unknown (red) values — indicating the system is being initialized.
Once reset goes low (logic 0), the design begins normal operation and the output stabilizes with valid logic values.

### 3. Clocking
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/period_sim.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>  

>The period signal from the PLL block remains constant at approximately 35.4 ns, confirming a stable and continuous clock throughout the simulation.
This ensures all modules within the BabySoC operate synchronously and in phase

### 4. Dataflow between modules 
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_2/task_2/dataflow_in_modules.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>  

>The RVMYTH processor acts as the core computational block, with its r17 register storing data values sent to the DAC (Digital-to-Analog Converter).
As RVMYTH executes instructions, r17 sequentially updates data, forming a continuous stream towards the DAC.
The combined operation of r17 and DAC output confirms correct data transfer and synchronization between modules.

---

## Conclusion
This task successfully demonstrates functional simulation of the BabySoC using open-source tools. The observed waveforms validate correct system initialization, stable clock generation, and coherent data exchange between modules.
Through this exercise, the key concepts of SoC reset mechanisms, clock domain stability, and inter-module dataflow were clearly understood and verified.
