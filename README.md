# 🖥️ RISC-V Reference SoC Tapeout Program VSD

<div align="center">

![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)
![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)
![Participants](https://img.shields.io/badge/Participants-3500+-success?style=for-the-badge)
![India](https://img.shields.io/badge/Made%20in-India-saffron?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHJlY3Qgd2lkdGg9IjI0IiBoZWlnaHQ9IjgiIGZpbGw9IiNGRjk5MzMiLz4KPHJlY3QgeT0iOCIgd2lkdGg9IjI0IiBoZWlnaHQ9IjgiIGZpbGw9IiNGRkZGRkYiLz4KPHJlY3QgeT0iMTYiIHdpZHRoPSIyNCIgaGVpZ2h0PSI4IiBmaWxsPSIjMTM4ODA4Ii8+Cjwvc3ZnPgo=)

</div>

Welcome to my journey through the **SoC Tapeout Program VSD**!

This repository documents my **week-by-week progress** with tasks inside each week.

<div align="center">

> *"In this program, we learn to design a System-on-Chip (SoC) from basic RTL to GDSII using open-source tools. Part of India's largest collaborative RISC-V tapeout initiative, empowering 3500+ participants to build silicon and advance the nation's semiconductor ecosystem."*

</div>

<div align="center">

```
📝 RTL Design → 🔄 Synthesis → 🏗️ Physical Design → 🎯 Tapeout Ready
```

</div>

---
## 📅 **Week 0 — Setup & Tools**

<details>
<summary><b>🛠️ Foundation Week (week-0) : Environment Setup and Tool Installation</b></summary>

This week focuses on preparing the development environment with essential open-source EDA tools for the complete RTL-to-GDSII flow.

### 🛠️ **Tasks Overview**

| Task | Description | Tools Installed | Status |
|------|-------------|----------------|---------|
|**Task 1** | [Summary](https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_0/task_1/Summary) | **video explanined** | ✅ Done |
| **Task 2** | 🛠️ [Tools & Environment Setup](https://github.com/vivek-kosigi/RTL2GDS_VSD/tree/main/Week_0/task_2) | **Complete EDA Toolchain Setup** | ✅ Done |



#### **Core RTL Design & Synthesis Tools**

| Tool | Purpose | Verification |
|------|---------|--------------|
| 🧠 **Yosys** | RTL Synthesis & Logic Optimization | ✅ Done |
| 📟 **Iverilog** | Verilog Simulation & Compilation | ✅ Done |
| 📊 **GTKWave** | Waveform Viewer & Analysis | ✅ Done |
| ⚡ **Ngspice** | Analog & Mixed-Signal Simulation | ✅ Done |
| 🎨 **Magic VLSI** | Layout Design & DRC Verification | ✅ Done |

#### **Advanced Flow Tools**

| Tool | Purpose | Verification |
|------|---------|--------------|
| 🐳 **Docker** | Containerization Platform | pending |
| 🌊 **OpenLane** | Complete RTL-to-GDSII Flow | pending |

### 🌟 **Key Learnings from Week 0**

- **Successfully installed** and verified **open-source EDA tools** ecosystem
- **Mastered environment setup** for professional RTL design and synthesis workflows
- **Prepared comprehensive system** for upcoming **RTL → GDSII flow experiments**
- **Established Docker-based** OpenLane environment for automated design flows
- **Configured virtual machine** with optimal specifications for EDA workloads

</details>

## 🎯 **Program Objectives & Scope**

| Aspect | Details |
|--------|---------|
| 🎓 **Learning Path** | Complete SoC Design: RTL → Synthesis → Physical Design → Tapeout |
| 🛠️ **Tools Focus** | Open-Source EDA Ecosystem (Yosys, OpenLane, Magic, etc.) |
| 🏭 **Industry Relevance** | Real-world semiconductor design methodologies |
| 🤝 **Collaboration** | Part of India's largest RISC-V tapeout initiative |
| 📈 **Scale** | 3500+ participants contributing to silicon advancement |
| 🇮🇳 **National Impact** | Advancing India's semiconductor ecosystem |

</div>

---

## 📅 **Week 1 — RTL Simulation & Synthesis**

  
  <summary><b>🔹 Overview: Week 1 Tasks</b></summary>

  This week focuses on **practical RTL simulation, synthesis, and post-synthesis verification** using open-source EDA tools.

  ### 🛠️ **Tools Used**

  | Tool | Purpose |
  |------|---------|
  | 🧠 **Yosys** | RTL Synthesis & Logic Optimization |
  | 📟 **Iverilog** | RTL Simulation & Compilation |
  | 📊 **GTKWave** | Waveform Analysis |
  | 📦 **Lib Files** | Standard cell library for technology mapping |
  
  ### 🔹 **Daily Topics**
  
  | Day | Concept Focus |
  | -----|---------------|
  | Day 1 | RTL Simulation, Multiplexer design, Basic Synthesis |
  | Day 2 | `.lib` files, Hierarchical vs Flat Synthesis, Flip-Flop coding, RTL Optimizations |
  | Day 3 | Combinational & Sequential Logic Optimizations, Retiming, State Reduction |
  | Day 4 | Gate-Level Simulation, Synthesis-Simulation Mismatch, Coding Best Practices |
  | Day 5 | Optimization in Synthesis |

  ### ✅ **Work Completion Tracker**

  | Work | Completion |
  |------|------------|
  | Simulation | ✅ Done |
  | Synthesis | ✅ Done |
  | Post-Synthesis Simulation | ✅ Done |
  | Creation of GitHub repo with data | ✅ Done |

  **Key Takeaways:**

  - RTL simulation verifies logic before hardware implementation.  
  - Synthesis converts RTL to gate-level netlist using `.lib` cells.  
  - Post-synthesis simulation ensures functional correctness.  
  - Understanding `.lib` files, hierarchical design, and flip-flop coding is critical for real-world ASIC design.

  
---

## 📅 **Week 2 — BabySoC Fundamentals & Functional Modelling **

This week focused on **SoC fundamentals** and performing **functional modelling of BabySoC**.  

📘 **Highlights**  
- Studied **SoC basics**: CPU, memory, peripherals, and interconnects.  
- Understood BabySoC architecture (RVMYTH core + PLL + DAC).  
- Learned the role of **functional modelling** before RTL & physical design.  
- Cloned the **VSDBabySoC repo** and converted `.tlv → .v` using Sandpiper.  
- Simulated BabySoC with **Icarus Verilog** and analyzed signals in **GTKWave**.  

📊 **Key Results**  
- Reset releases → signals stabilize and operation begins.  
- PLL generates a stable ~35.4 ns clock.  
- RVMYTH feeds continuous data to DAC → confirms correct dataflow.  

✅ **Takeaways**  
- Stronger grasp of **SoC integration concepts**.  
- Hands-on with **simulation + waveform verification**.  
- Experience with **TL-Verilog → Verilog → Simulation workflow**.  
---

# 🧩 Week 3: Synthesis, GLS & STA

This week centers on the critical post-RTL stages of chip design, where the abstract Verilog code is transformed into a concrete gate-level representation. The focus is on ensuring that the synthesized design not only functions correctly but also meets required timing constraints for reliable operation.

---

## Tasks Overview

- **Task 1 – Synthesis & GLS:**  
  Performed synthesis using the Yosys tool to convert RTL Verilog code into a gate-level netlist mapped to standard cell libraries. Verified functional correctness at the gate level through Gate-Level Simulation (GLS), accounting for real delays and interconnect timing to ensure the design behaves as intended after synthesis.

- **Task 2 – STA Theory:**  
  Studied the foundational concepts of Static Timing Analysis (STA), including setup and hold timing checks, understanding timing paths (launch and capture paths), and how slack is computed to assess if signals meet timing deadlines. This theoretical knowledge is essential for timing closure in complex designs.

- **Task 3 – OpenSTA Practical:**  
  Applied hands-on STA using the OpenSTA tool by analyzing actual timing reports generated from synthesized designs. Learned how to interpret timing constraints, analyze path delays, and identify critical paths and violations to optimize the design timing.

---

# 🧠 Week 4: CMOS Device Characterization & Robustness Evaluation


Welcome to **Week 4** of the **VSD SoC Design Journey**, where we explored **device-level CMOS fundamentals** using **SPICE simulations**.  
This week’s focus was to understand transistor behavior, inverter characteristics, switching dynamics, and robustness under power and device variations.

---

## 🧩 Overview

| Focus Area | Key Topics Covered |
|-------------|--------------------|
| **Day 1** | NMOS Drain Current Characteristics & SPICE Introduction |
| **Day 2** | Velocity Saturation & CMOS Inverter VTC |
| **Day 3** | Switching Threshold & Dynamic Simulations |
| **Day 4** | Noise Margin & Robustness Evaluation |
| **Day 5** | Power Supply and Device Variation Analysis |

---

## ⚙️ Tools & Environment

| Tool | Purpose |
|------|----------|
| **ngspice** | Circuit-level simulation |
| **Python** | Script support and data analysis |
| **Sky130 PDK** | Process Design Kit for simulation |
| **Git** | Repository cloning and version control |

Repository used: [sky130CircuitDesign](https://github.com/kunalg123/sky130CircuitDesign)

---

## 🧠 Key Skills Developed

- Mastery of the complete synthesis flow from RTL to gate-level netlist using open-source tools.  
- Experience in Gate-Level Simulation to validate post-synthesis functionality with accurate timing.  
- In-depth understanding of Static Timing Analysis principles and practical usage of OpenSTA for timing validation.

---

By completing this week’s activities, you will bridge the gap between RTL behavioral design and gate-level implementation, gaining insights critical for real-world chip design and timing closure.


---
## 🙏 **Acknowledgment**

<div align="center">

### 🏆 **Program Leadership & Support**

I am thankful to [**Kunal Ghosh**](https://github.com/kunalg123) and Team **[VLSI System Design (VSD)](https://vsdiat.vlsisystemdesign.com/)** for the opportunity to participate in the ongoing **RISC-V SoC Tapeout Program**.



## 📈 **Weekly Progress Tracker**

![Week 0](https://img.shields.io/badge/Week%200-Tools%20Setup-success?style=flat-square)
![Week 1](https://img.shields.io/badge/Week%201-RTL%20Simulation%20&%20Synthesis-lightgrey?style=flat-square)
![Week 2](https://img.shields.io/badge/Week%202-VSDBabySOC-success?style=flat-square)  
![Week 3](https://img.shields.io/badge/Week%203-STA-lightgrey?style=flat-square)
![Week 4](https://img.shields.io/badge/Week%204-Circuit%20Designing%20-success?style=flat-square)
![Week 5](https://img.shields.io/badge/Week%205-Upcoming-lightgrey?style=flat-square)
![Week 6](https://img.shields.io/badge/Week%206-Next%20soon-success?style=flat-square)

### 🚀 **Journey Continues...**

Stay tuned for upcoming weeks covering RTL design, synthesis, physical design, and final tapeout preparation!

---
