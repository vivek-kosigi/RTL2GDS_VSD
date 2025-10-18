# ⚡ Day 5: CMOS Power Supply & Device Variation Robustness Evaluation

---

## 📘 Concepts Learned
This day focuses on analyzing how **CMOS circuit performance** changes due to **power supply variations** and **device-level mismatches**.  
Both factors significantly affect **gain**, **speed**, and **robustness** in modern, scaled semiconductor technologies.

---

## 🧩 1. Power Supply Scaling

**Power supply scaling** involves reducing the **supply voltage (VDD)** to improve power efficiency.  
While it reduces power consumption and can improve gain to some extent, excessive scaling can degrade the **switching ability** and **speed** of the transistor.

### Simulation Setup
Two SPICE simulations were performed using the **same MOS device**:

| Device | W (µm) | L (µm) | VDD (V) |
|----------|---------|---------|----------|
| Device 1 | 0.9 | 0.3 | 2.5 |
| Device 2 | 0.9 | 0.3 | 1.0 |

The objective is to study how changing **VDD** affects the **Voltage Transfer Characteristic (VTC)** and **gain**.

---

## ⚙️ SPICE Simulation Procedure (Lab 1)

### Run the Simulation
```txt
ngspice day5_inv_supplyvariation_Wp1_Wn036.spice
```

### Plot the Waveform
```txt
plot out vs in
```

### Compute Gain \(A_V\)

Gain is calculated from the **slope of the VTC curve**:
```txt
AV ​= ΔVin​ / ΔVout​​ =  y0​(1)−y0​(2)​ / x0​(1)−x0​(2)
```

**Example Calculation:**

| Parameter | Expression | Value |
|------------|-------------|--------|
| \(y_0(1) - y_0(2)\) | Output voltage difference | 1.598085 |
| \(x_0(1) - x_0(2)\) | Input voltage difference | 0.214788 |
| **Gain \(A_V\)** | \(1.598085 / 0.214788\) | **7.4402** |

---

### Observation Across Different Supply Voltages

| VDD (V) | Gain \(A_V\) | Observation |
|----------|---------------|-------------|
| 2.5 | 7.38 | Baseline |
| 2.0 | ~8.1 | Slight improvement |
| 1.5 | ~9.5 | Noticeable improvement |
| 1.0 | ~10.8 | High gain |
| 0.5 | 11.53 | Maximum observed gain |

**Result:**  
There is approximately **56% improvement** in gain as **VDD** scales down from **2.5 V** to **0.5 V**.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_5/images/day5_sv_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_5/images/day5_sv_value.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## ⚖️ Trade-offs in Power Supply Scaling

| Advantages | Disadvantages |
|-------------|---------------|
| ✅ Increased Gain | ⚠️ Reduced speed/performance |
| ✅ Reduced Power Consumption | ⚠️ Risk of transistor not switching properly |
| ✅ Lower Energy Usage | ⚠️ Increased delay due to slower charge/discharge |

**Summary:**  
Power scaling enhances **energy efficiency**, but excessive reduction can lead to **slower switching** and **reduced performance**.

---

## 🧩 2. Device Variation

**Device variation** originates from **manufacturing process differences** that impact transistor parameters like **W/L ratio**, **oxide thickness**, and **threshold voltage**.  
These variations cause fluctuations in **drain current**, **switching threshold**, and **noise margins**, making variation analysis **essential for robust design**.

### Sources of Variation

| Source | Description | Impact |
|---------|--------------|--------|
| **Etching Process Variation** | Alters transistor dimensions (W/L) | Affects drain current \(I_d\) |
| **Oxide Thickness Variation** | Changes oxide capacitance \(C_{ox}\) | Impacts current and delay |
| **Device Strength Imbalance** | Uneven PMOS/NMOS drive strength | Shifts switching threshold \(V_m\) |

Such variations may cause **timing mismatches**, **functional errors**, and **reduced yield** if unaddressed during design.

---

## ⚙️ SPICE Simulation Procedure (Lab 2)

### Run the Simulation
```txt
ngspice day5_inv_devicevariation_wp7_wn042.spice
```

### Plot for Comparison
```txt
plot out vs in
```
- Strong PMOS – Weak NMOS  
- Weak PMOS – Strong NMOS  

Observe and compare how the **switching point (\(V_m\))** shifts with device strength imbalance.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_5/images/day5_dv_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_5/images/day5_dv_value.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## 📊 Observations

- As **VDD decreases**, the **gain increases** initially due to reduced current saturation and higher voltage sensitivity.  
- Beyond a certain limit, **gain saturates** because lower voltage cannot fully turn on transistors.  
- **Device mismatches** cause the inverter’s **VTC curve** to shift, altering the **switching threshold** and **noise margins**.  
- **SPICE simulations** illustrate how both **power scaling** and **device imbalance** impact **circuit robustness**.

---

## 💡 Applications
- Low-power **CMOS design** and **energy-efficient SoCs**  
- Robust **digital logic** for scaled technologies  
- **Variation-aware timing and noise modeling** in EDA tools

---

## ✅ Key Takeaways
- **Power supply scaling** enhances **energy efficiency** and **gain**, but may reduce **switching performance**.  
- **Device variations** are inherent in fabrication and must be evaluated for **reliable circuit operation**.  
- **SPICE simulations** provide visibility into transistor-level effects influencing **system robustness**.  
- Maintaining a **balanced VDD** and **matched PMOS/NMOS sizing** ensures **stable inverter behavior**.

---
