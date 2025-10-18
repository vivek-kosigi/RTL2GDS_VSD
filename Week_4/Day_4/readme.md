# 🧩 Day 4: CMOS Noise Margin & Robustness Evaluation

---

## 📘 Concepts Learned

### 🔹 Static Behavior Evaluation — Noise Margin
In an ideal digital inverter, the output instantly switches between logic **HIGH (1)** and **LOW (0)**.  
However, in real CMOS circuits, signal transitions are not perfectly sharp — they have **finite slopes** due to transistor behavior and **parasitic effects**.  

This gradual transition introduces **uncertainty regions** around the switching point, which can make digital circuits **sensitive to noise**.  
To ensure reliable logic operation, **noise margins** are defined.

---

## 🧠 Understanding Noise Margin

### Voltage Levels

| Symbol | Meaning | Description |
|---------|----------|-------------|
| **VIL** | Input Low Voltage | Maximum input voltage recognized as logic ‘0’ |
| **VIH** | Input High Voltage | Minimum input voltage recognized as logic ‘1’ |
| **VOL** | Output Low Voltage | Output voltage level when logic ‘0’ is driven |
| **VOH** | Output High Voltage | Output voltage level when logic ‘1’ is driven |

### VTC Behavior
In the **Voltage Transfer Characteristic (VTC)** curve:
- For **input 0 → VIL**, the output remains stable at **VOH (logic 1)**.
- For **input VIH → VDD**, the output settles at **VOL (logic 0)**.
- Between **VIL and VIH**, the inverter transitions gradually.

### Noise Margins
To tolerate unwanted signal fluctuations:
- **Noise Margin High (NMH):** Maximum noise that a logic HIGH can tolerate.  
- **Noise Margin Low (NML):** Maximum noise that a logic LOW can tolerate.

---

## 🧾 Formulas
```txt
NM_H = VOH - VIH  
NM_L = VIL - VOL
```

---

## ⚙️ SPICE Simulation Setup
The experiment analyzes how **PMOS/NMOS sizing (W/L ratio)** affects **noise margin** and **switching point**.

| Case | PMOS/NMOS Ratio (Wp/Lp : Wn/Ln) |
|------|----------------------------------|
| 1 | 1:1 |
| 2 | 2:1 |
| 3 | 3:1 |
| 4 | 4:1 |
| 5 | 5:1 |

Each case was **simulated using SPICE** to extract **VTC curves** and measure **VIL, VIH, VOL, VOH**, and the resulting **noise margins**.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_4/images/day4_different_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## 🧪 Lab Procedure

### Steps
1. **Run the SPICE simulation:**
```txt
ngspice day4_inv_noisemargin_wp1_wn036.spice
```

2. **Plot the waveform:**
```txt
plot out vs in
```

3. Identify the **slope = –1** points on the VTC curve to find **VIL** and **VIH**.  
4. Extract and record voltage levels:

## Result 

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_4/images/day4_wave.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_4/images/day4_values.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

| Parameter | Value (V) |
|------------|-----------|
| **VOH** | 1.71915 |
| **VIH** | 0.96875 |
| **VOL** | 0.144681 |
| **VIL** | 0.765625 |

### Noise Margin Calculation

| Parameter | Formula | Calculation | Result (V) |
|------------|----------|-------------|-------------|
| **NMH** | VOH – VIH | 1.71915 – 0.96875 | **0.7504** |
| **NML** | VIL – VOL | 0.765625 – 0.144681 | **0.6209** |

---

## 📊 Observations & Insights
- The **VTC curve** shows a smooth transition between **VOH** and **VOL**, with a small slope around the switching region.  
- Increased **PMOS sizing (Wp/Lp)** slightly increases both **NMH** and **NML**, boosting **noise robustness**.  
- A balanced inverter design ensures **NMH ≈ NML**, giving **equal logic tolerance** for HIGH and LOW levels.  
- Higher noise margins increase **signal integrity**, **stability**, and **reliability** in digital circuits.

---

## 💡 Applications
Noise margin analysis is crucial in:
- Amplifiers  
- Memory cells (**SRAM**, **DRAM**)  
- Logic buffers  
- Timing-critical paths in **high-speed systems**

---

## ✅ Key Takeaways
- **Noise Margin** defines a circuit’s ability to tolerate voltage fluctuations.  
- Larger **NMH** and **NML** values imply **stronger robustness**.  
- Adjusting **transistor W/L ratios** helps optimize inverter **symmetry** and **performance**.  
- **SPICE simulations** effectively visualize the analog effects influencing digital behavior.

---
