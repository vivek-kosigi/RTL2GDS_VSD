# ⚡ Day 3: CMOS Switching Threshold & Dynamic Simulations

---

## 📘 Concepts Learned

### 🔹 SPICE Deck Creation
To simulate CMOS circuits, a **SPICE deck** (simulation input file) defines key parameters:

- **Component connectivity:** How PMOS and NMOS are connected.  
- **Component values:** Transistor W/L ratios and supply parameters.  
- **Node identification:** All circuit nodes are labeled clearly (e.g., input, output, VDD, ground).

**Example SPICE line:**
```txt
M1 out in vdd vdd pmos W=1.8 L=1.2
```

This line defines a **PMOS transistor (M1)** connected between **VDD** and **output**, with **input** as its gate and the specified **width/length ratios**.

---

## 🧪 Lab Experiments

### 1. Static Behavior Analysis

**Objective:**  
To determine the **switching threshold (Vm)** — the voltage at which **Vin = Vout**.  
At this point, both transistors conduct partially, defining the **inverter’s transition point**.

#### Operation Cases in Inverter Transfer Region

| Case | PMOS       | NMOS       |
|------|-------------|------------|
| 1    | Linear      | Off        |
| 2    | Linear      | Saturation |
| 3    | Saturation  | Saturation |
| 4    | Saturation  | Linear     |
| 5    | Off         | Linear     |

#### Simulation Study: Transistor Sizing and Vm Variation

| Case | PMOS/NMOS Ratio (Wp/Lp : Wn/Ln) | Observation              |
|------|----------------------------------|---------------------------|
| 1    | 1:1                              | Balanced switching       |
| 2    | 2:1                              | Shifted threshold        |
| 3    | 3:1                              | Faster rise              |
| 4    | 4:1                              | Reduced fall delay       |
| 5    | 5:1                              | Dominant PMOS drive      |

**Result:**  
Larger **PMOS sizes (higher Wp/Lp)** increase **Vm** and improve **rise delay performance**, though an imbalance may cause asymmetry between **rise** and **fall times**.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_3/images/day3_different_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

### 2. Dynamic Behavior Analysis

**Objective:**  
Evaluate the **transient (time-domain) response** of the CMOS inverter.

#### Simulations Performed
- `day3_vtc` → Voltage Transfer Characteristics
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_3/images/day3_vts_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

- `day3_trans` → Transient Analysis (Vin vs. Vout over time)
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_3/images/day3_trans_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

#### Measured Delays
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_3/images/day3_vtc_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_3/images/day3_trans_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

| Type | x0(1) (ns) | x0(2) (ns) | Delay (ns) |
|------|-------------|-------------|-------------|
| **Rise Delay (tr)** | 2.47714 | 2.14857 | 0.32857 |
| **Fall Delay (tf)** | 4.33659 | 4.04634 | 0.29025 |

**Observations:**
- **Rise and fall delays** are nearly symmetrical when **Wp/Lp ≈ 2 × Wn/Ln**.  
- Delay differences reflect **transistor strength mismatch** (PMOS typically weaker than NMOS).

---

## ⚙️ Analysis Summary

| Parameter | Description |
|------------|-------------|
| **Vm (Switching Threshold)** | Voltage where Vin = Vout; defines inverter’s switching point |
| **Rise Delay (tr)** | Time for output to rise from 10% to 90% of VDD |
| **Fall Delay (tf)** | Time for output to fall from 90% to 10% of VDD |
| **Impact of W/L Ratios** | Larger PMOS width improves rise delay and increases Vm |

---

## ✅ Key Takeaways
- **SPICE deck** defines all circuit connectivity and simulation details.  
- **Switching threshold (Vm)** determines the **logic transition region** of the inverter.  
- **Rise/Fall delay** aids in analyzing **inverter speed** and **symmetry**.  
- **Transistor sizing** strongly influences both **static** and **dynamic** performance of CMOS circuits.

---

