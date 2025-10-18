# 🧠 Day 2: Velocity Saturation & CMOS Inverter VTC

---

## 📘 Concepts Learned

### 🔹 Velocity Saturation

**Objective:**  
To study how MOSFET behavior transitions from **quadratic** to **linear** current dependence as the **channel length decreases**.

#### 🧪 Simulation Summary
- Performed **SPICE simulations** for different technology nodes (varied **W/L ratios**).  
- Compared resulting **Id–Vds curves** for **long-channel** and **short-channel** devices.

#### 🧩 Observations
- **Long-channel devices (>250 nm):** Show **quadratic dependence** in the Id–Vds plot.  
- **Short-channel devices (<250 nm):** Show **linear dependence** due to **velocity saturation**.

#### ⚙️ Physical Explanation
- As the **electric field (E)** increases, the carrier velocity (**v**) stops increasing linearly and reaches a **saturation point**.  
- Relation at low fields:
  ```txt
  v = μ × E
  ```

- Beyond a critical field, the velocity **saturates**, causing **early current saturation** in short-channel devices.

#### 🧮 Current Relation
```txt
ID​=−vn​(x)⋅Qi​(x)⋅W
```

This relation represents the drain current in terms of carrier velocity and charge density.

#### ⚡ Modes of Operation

| Channel Type | Operation Modes |
|---------------|----------------|
| **Long Channel (>250 nm)** | Cutoff, Resistive, Saturation |
| **Short Channel (<250 nm)** | Cutoff, Resistive, Velocity Saturation, Saturation |

**Observation:**  
Velocity saturation causes **early saturation** in output characteristics, resulting in **lower peak current**.

---

## ⚙️ Lab Work

### Simulated & Analyzed
- **Id–Vds characteristics:** Drain Current vs. Drain Voltage  
- **Id–Vgs characteristics:** Drain Current vs. Gate Voltage  

### Waveform 
the waveform of vgs
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_2/images/day2_vds.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
the values of points from vgs graph
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_2/images/day2_vds_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
the waveform of vds
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_2/images/day2_vgs.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

### Comparison
- Visualized the **impact of velocity saturation** by comparing **long-channel** and **short-channel** MOSFET curves.  
- Observed how saturation limits drain current growth in short-channel devices.

---

## ⚡ CMOS Inverter Voltage Transfer Characteristics (VTC)

### 🔸 Concept Overview
A **CMOS inverter** behaves as a **digital switch** in logic circuits.

| Input (Vin) | PMOS | NMOS | Output (Vout) Behavior |
|--------------|-------|-------|------------------------|
| HIGH | OFF | ON | Output capacitor discharges to ground |
| LOW | ON | OFF | Output capacitor charges from VDD |

### 🔸 Voltage & Current Relations
- The **drain current (Id)** vs. **drain voltage (Vds)** relationship determines transistor switching.  
- To plot the **VTC (Voltage Transfer Characteristic):**
  1. Express **PMOS gate-source voltage (Vgs_p)** as a function of **Vin**.  
  2. Express **PMOS & NMOS drain-source voltages (Vds_p, Vds_n)** in terms of **Vout**.  
  3. **Merge both load curves** to obtain the inverter transfer characteristic (VTC).

---

## ✅ Key Takeaways
- **Velocity saturation** reduces **current drive capability** in short-channel MOSFETs.  
- **CMOS inverter behavior** depends on the complementary operation of PMOS and NMOS transistors.  
- The **transition region** in the inverter’s **VTC** defines **noise margins** and **switching thresholds**, critical for reliable digital design.

---
