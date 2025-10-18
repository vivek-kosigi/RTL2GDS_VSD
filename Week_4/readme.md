# 🧠 Week 4: CMOS Circuit Design (sky130-style)

Welcome to Week 4 of the VLSI System Design (VSD) training program.
This folder contains

- Day 1 NMOS Drain Current (Id) vs Drain-Source Voltage (Vds)  
- Day 2 Velocity Saturation & CMOS Inverter VTC  
- Day 3 CMOS Switching Threshold & Dynamic Simulations  
- Day 4 CMOS Noise Margin & Robustness Evaluation  
- Day 5 CMOS Power Supply & Device Variation Robustness  

---

### 🔹 Day 1: NMOS Drain Current (Id) vs Drain-Source Voltage (Vds)

#### Concepts Covered
- Basics of NMOS and PMOS transistor structure  
- Threshold voltage (Vth), depletion region, inversion  
- Linear and saturation regions of operation  
- SPICE simulation fundamentals  

#### Key Questions Explored
- Where does cell delay originate?
- How accurate are delay calculations?
- How to verify STA correctness using SPICE?

#### Lab Work
```txt
git clone https://github.com/kunalg123/sky130CircuitDesign
ngspice day1_nfet_idvds_L2_W5.spice
plot -vdd#branch
```

Observed the **Id–Vds** characteristics and studied current behavior across voltage variations.

**Takeaway:**  
SPICE enables delay and W/L ratio analysis.  
Even identical buffers can have varying delays due to geometry differences.

---

### 🔹 Day 2: Velocity Saturation & CMOS Inverter VTC

#### Concepts Covered
- Velocity saturation in short-channel MOSFETs (<250 nm)  
- Current dependence on mobility and electric field  
- CMOS inverter **Voltage Transfer Characteristics (VTC)**  
- Merging NMOS/PMOS load curves  

#### Theory
| Device Type | Operation Modes |
|--------------|----------------|
| Long Channel | Cutoff, Resistive, Saturation |
| Short Channel | Cutoff, Resistive, Velocity Saturation, Saturation |

**Current Equation:**
```txt
Id​ = kn​[(Vgt​Vmin​)−(Vmin2​/2)] (1+λVds​)
```

#### Lab Work
- Simulated MOSFETs across technology nodes with different W/L ratios  
- Plotted **Id–Vds** and **Id–Vgs** curves  
- Generated and analyzed CMOS inverter VTC curves
```txt
ngspice day2_nfet_idvds_L015_W039.spice
ngspice day2_nfet_idvgs_L015_W039.spice
```

**Observation:**  
Velocity saturation causes earlier current saturation.  
Current behavior transitions from **quadratic** to **linear** with scaling.

---

### 🔹 Day 3: CMOS Switching Threshold & Dynamic Simulations

#### Concepts Covered
- SPICE deck and netlist creation  
- Node naming and transistor parameter assignment  
- Inverter switching threshold (Vm) and rise/fall delay analysis  

#### Static Behavior
At **Vin = Vout = Vm**, both transistors conduct partially.  
Simulated with multiple **PMOS/NMOS ratios**:

| Ratio | Configuration |
|--------|----------------|
| 1:1 | Balanced |
| 2:1 | Shifted Vm |
| 3:1 | Faster rise |
| 4:1 | Reduced fall delay |
| 5:1 | Dominant PMOS drive |

#### Dynamic Simulation
```txt
ngspice day3_inv_vtc_Wp084_Wn036.spice
ngspice day3_inv_tran_Wp084_Wn036.spice
```

**Results:**
| Parameter | Value (ns) |
|------------|-------------|
| Rise Delay | 0.32857 |
| Fall Delay | 0.29025 |

**Takeaway:**  
Changing **W/L ratio** modifies **Vm** and affects delay balance.  
Fluctuation analysis helps optimize inverter switching symmetry.

---

### 🔹 Day 4: CMOS Noise Margin & Robustness Evaluation

#### Concepts Covered
- **Noise Margin (NML & NMH)** in digital logic  
- Voltage levels: **VIL**, **VIH**, **VOL**, **VOH**  
- Importance of slope = -1 points in VTC curve  

#### Theory
For stable logic behavior:
- Input < VIL → Logic ‘0’
- Input > VIH → Logic ‘1’

**Formulas:**
\[
NM_H = VOH - VIH
\]
\[
NM_L = VIL - VOL
\]

#### SPICE Simulation
```txt
ngspice day4_inv_noisemargin_wp1_wn036.spice
```

**Measurements:**
| Parameter | Formula | Result (V) |
|------------|----------|-------------|
| NMH | VOH – VIH = 1.71915 – 0.96875 | 0.7504 |
| NML | VIL – VOL = 0.765625 – 0.144681 | 0.6209 |

**W/L Variations:** Same as Day 3 (from 1:1 to 5:1)

**Applications:**  
Used in **amplifiers**, **memory cells**, and **logic buffers** for stable digital design.

**Takeaway:**  
Higher PMOS/NMOS ratios improve both **NMH** and **NML**, ensuring noise robustness.

---

### 🔹 Day 5: CMOS Power Supply & Device Variation Robustness

#### Concepts Covered
- Impact of **VDD scaling** on gain and performance  
- Analysis of **device variation** from fabrication processes  

#### Power Supply Scaling

**Simulated same MOSFET** across varying VDD levels:

| VDD (V) | Gain (A_V) | Observation |
|----------|-------------|--------------|
| 2.5 | 7.38 | Baseline |
| 2.0 | ~8.1 | Slight improvement |
| 1.5 | ~9.5 | Noticeable improvement |
| 1.0 | ~10.8 | High gain |
| 0.5 | ~11.53 | Maximum gain |

→ **~56% gain improvement** observed when scaling down **VDD from 2.5 V to 0.5 V**.

**Trade-offs:**

| Advantages | Disadvantages |
|-------------|----------------|
| ✅ Increased gain | ⚠️ Reduced performance |
| ✅ Lower energy usage | ⚠️ Slower switching |
| ✅ Reduced power | ⚠️ Potential instability |

#### Device Variation Analysis

**Variation Sources:**

| Source | Description | Impact |
|---------|--------------|--------|
| Etching Process | Alters dimensions | Changes \(I_d\) |
| Oxide Thickness | Variations in \(C_{ox}\) | Impacts delay |
| Strength Imbalance | Uneven PMOS/NMOS | Shifts \(V_m\) |

#### Lab Work
```txt
ngspice day5_inv_supplyvariation_Wp1_Wn036.spice
ngspice day5_inv_devicevariation_wp7_wn042.spice
```

Analyzed VTC shift due to **strong/weak** transistor mismatches and gain variation.

**Takeaway:**  
Lowering VDD can increase gain but reduces switching speed.  
Device mismatch analysis ensures robust design across fabrication variability.

---

## 🧾 Final Learnings

✅ Understood **transistor-level operations** through hands-on SPICE simulations.  
✅ Derived **I–V characteristics**, **VTC curves**, **delays**, and **noise margins**.  
✅ Explored **velocity saturation**, **power scaling**, and **device variation** effects.  
✅ Gained confidence in **analog verification** and **robust CMOS design** techniques.

---

## 📎 Deliverables
- `.cir` / `.net` simulation files for all 5 days  
- `.raw` waveform data and `.png` plots  
- Computed parameters: **Delay**, **Gain**, **Vm**, **NMH**, **NML**  
- Detailed README for each day with lab notes and results  

---

