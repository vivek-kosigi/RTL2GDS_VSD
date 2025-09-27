# 🚀 Day 3: Combinational & Sequential Optimizations – In-Depth Analysis

---

## 🌟 Introduction

Optimization is key to achieving better **area efficiency**, **power savings**, and **higher clock frequencies** in digital circuits. On Day 3, we focused on practical optimization techniques for **combinational** and **sequential** logic, exploring their uses and impacts in real designs.

---

## ⚙️ Combinational Logic Optimization

### 🔍 Why Optimize Combinational Logic?

- **Squeeze the logic** to reduce chip area and dynamic power consumption.  
- Simplify Boolean functions for efficient hardware use.

### 1️⃣ Constant Propagation Optimization

Substitutes constant inputs directly into logic expressions to remove or simplify gates.

**Example:**  

If   
```
Y = ((A * B) + C)'

and (A = 0), then

Y = ((0 * B) + C)' = C'
```

This reduces gate count by removing logic related to \(A\).

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/comb_const_opt.png" 
       alt="Simulated Wavefrom of MUX" width="600"/>
</p>

### 2️⃣ Boolean Logic Optimizations

Uses algebraic laws and automated algorithms to simplify Boolean logic, minimizing gate usage and improving speed.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/boolean_opt.png" 
       alt="Simulated Wavefrom of MUX" width="600"/>
</p>

---

## 🔄 Sequential Logic Optimization

### 1️⃣ Constant Propagation in Sequential Logic

If a flip-flop's input \(D\) is constant, output \(Q\) reaches that constant, possibly eliminating redundant logic unless asynchronous controls are present.

### 2️⃣ State Optimizations

Minimizes finite state machines by removing unused states and merging equivalent ones to simplify logic and reduce flip-flop counts.

### 3️⃣ Retiming

Repositions flip-flops across combinational paths to balance delays, decreasing critical path length and boosting clock frequency.

**Example:**  
Original delays: 5ns and 2ns ⇒ max frequency ≈ 200 MHz  
Balanced delays: 4ns and 3ns ⇒ max frequency ≈ 250 MHz  
Latency unchanged, throughput improved.

### 4️⃣ Sequential Logic Cloning

Replicates flip-flops driving many loads to reduce fanout delay and fix timing violations by distributing the load.

---

## 🛠 Lab Activities

## Combinational Designs

- Synthesized six designs: `opt_check`, `opt_check2`, `opt_check3`, `opt_check4`, `multiple_module_opt`, and `multiple_module_opt2`.
- Observed how synthesis uses basic gates (AND, OR, 3-input AND, XNOR) and manages multiple modules to implement multiplexers.

### Combinational Synthesis Results

Here we only synthesised 6 codes 

1. opt_check =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/opt_check_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

2. opt_check2 =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/opt_check2_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

3. opt_check3 =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/opt_check3_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

4. opt_check4 =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/opt_check4_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

5. multiple_module_opt =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/multi_opt_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

6. multiple_module_opt2 =
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/multi_opt2_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>


## Sequential Designs

- Simulated and synthesized `diff_const3`, `diff_const4`, `diff_const5`.
- Verified constant propagation and sequential logic optimizations.

### Sequential Simulaton & Synthesis Results

Here we simulated & synthesised 3 codes 

  
1. d flipflop constant 1 =

<div style="display: flex; justify-content: space-around;">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const1_sim.png" alt="Simulation" width="45%">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const1_sch.png" alt="Schematic" width="45%">
</div>

  
2. d flipflop constant 2 =

<div style="display: flex; justify-content: space-around;">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const2_sim.png" alt="Simulation" width="45%">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const2_sch.png" alt="Schematic" width="45%">
</div>

  
3. d flipflop constant 3 =

<div style="display: flex; justify-content: space-around;">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const3_sim.png" alt="Simulation" width="45%">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const3_sch.png" alt="Schematic" width="45%">
</div>

4. d flipflop constant 4 =

<div style="display: flex; justify-content: space-around;">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const4_sim.png" alt="Simulation" width="45%">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const4_sch.png" alt="Schematic" width="45%">
</div>

5. d flipflop constant 5 =

<div style="display: flex; justify-content: space-around;">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const5_sim.png" alt="Simulation" width="45%">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/dff_const5_sch.png" alt="Schematic" width="45%">
</div>


## Unused Port Optimization

- Compared `counter_opt` (driving one output) to `counter_opt2` (driving all outputs).
- Noticed how tools prune unneeded logic to minimize area and power.

### Optimize Unused Ports

1. counter_opt =

<div align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/counter_opt_sch.png" alt="Simulation" width="50%">
</div>

2. counter_opt2 =
   
<div align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_3/images/counter_opt2_sch.png" alt="Simulation" width="50%">
</div>

---

## 📌 Summary

- **Constant propagation and Boolean simplification** streamline combinational circuits.  
- **State reduction, retiming, and cloning** enhance sequential performance and timing.  
- Synthesis tools automate these optimizations, saving design time and improving chip efficiency.

---
