# ⚡ Day 1: Basics of NMOS Drain Current & SPICE Simulation

## 🧠 Objective
To understand the **NMOS drain current (Id)** vs **drain-to-source voltage (Vds)** characteristics, simulate the circuit in **SPICE**, and observe device behavior in different regions of operation.

---

## 📘 Concepts Learned

### 🔹 Circuit Design & SPICE Simulation
- Designed basic logic circuits (**AND, OR, NOR, NOT**) using **NMOS** and **PMOS** transistors.  
- Used **SPICE simulation** to visualize waveforms and analyze:
  - Propagation delay  
  - W/L ratio impact  
  - Output voltage characteristics  
- **SPICE** is crucial in **Physical Design (PD) flows** for understanding and verifying cell delays and device performance.

### 🔹 Importance of Delay Verification
- Different buffers in a circuit have varying **input slew** and **output load**, leading to delay differences.  
- Even under identical I/O conditions, changing the **W/L ratio** causes timing variations.  
- **SPICE simulations** enable accurate **delay verification** and cross-check with **STA (Static Timing Analysis)**.

---

## ⚙️ NMOS & PMOS Fundamentals

| Parameter | NMOS | PMOS |
|------------|-------|-------|
| **Substrate** | P-type | N-type |
| **Body Connection** | Ground | VDD |
| **Terminals** | Source, Drain, Gate, Body | Source, Drain, Gate, Body |
| **Isolation** | SiO₂ regions separate adjacent transistors | SiO₂ regions separate adjacent transistors |
| **Gate Material** | Poly-Silicon | Poly-Silicon |

### 🔸 Threshold Voltage (Vth)
- When **Vgs = 0**, no conductive channel exists between source and drain.  
- As **Vgs** increases, negative charges accumulate below the gate, forming a **depletion region**.  
- Once **Vgs > Vth**, **inversion** occurs, creating a conductive channel.  
- The **drain current (Id)** depends on this channel formation and the applied **Vds**.

---

## 🔬 Regions of Operation

1. **Resistive (Linear) Region** – The transistor acts like a variable resistor, and Id increases almost linearly with Vds.  
2. **Saturation Region** – Id becomes nearly constant as the channel pinches off.  
3. **Pinch-Off Condition** – Occurs when Vds ≥ (Vgs − Vth); current saturates even with increased Vds.  
4. **Drift Current Analysis** – Helps understand carrier motion and NMOS conduction behavior.

---

## 🧪 Lab Experiment

### Steps Performed
1. **Cloned the GitHub Repository**  
  ```txt
  git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop
  ```

2. **Navigated to Day 1 Directory**  
  Contained the required **netlist** and **library** files.

3. **Execution Command**
  ```txt
  ngspice day1_nfet_idvds_L2_W5.spice
  ```

4. **Observed Output and Plotted Waveforms**
  ```txt
  plot -vdd#branch
  ```


### Outcome
- Successfully visualized **Id–Vds characteristics** of an NMOS transistor.  
- Observed the dependency between **biasing**, **device parameters**, and **delay performance**.

#### waveform :
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_1/day1_vds.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

to check the Id vs Vd at nearest to x-axis we have zoomed it 
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_4/Day_1/day1_zoomed.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## 🧾 Key Takeaways
- **SPICE simulations** provide accurate **delay modeling** for **STA verification**.  
- **W/L ratio**, **input slew**, and **output load** directly affect timing and performance.  
- Developed a **fundamental understanding** of **MOSFET operation**, essential in **device-level analysis and PD flows**.

---

