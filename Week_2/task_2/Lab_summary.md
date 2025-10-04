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

---

