
# 🚀 Day 4: Gate-Level Simulation (GLS) and Synthesis Simulation Mismatches

---

## 🔍 What is Gate-Level Simulation (GLS)?

Gate-Level Simulation (GLS) is the process of simulating a digital circuit **after synthesis**, using the **gate-level netlist (`netlist.v`)** along with the original **testbench code**. The main purpose is to verify that the functionality remains the same after technology mapping to standard cells.

- Since the netlist is composed of technology-specific cells, **.lib model files** (standard cell libraries) are provided to the simulator to fully understand cell behavior and timing.

---

## ⚠️ Common Causes of Synthesis-Simulation Mismatch

1. **Missing Sensitivity List**

   - Example: In a multiplexer with `select`, `i0`, and `i1` pins, if an `always` block is written as:  
      always @(sel)  
      the output only updates when `sel` changes, **ignoring changes in `i0` or `i1`**, which causes simulation and synthesis to diverge.

   - **Fix:** Use the complete sensitivity list or use:  
      always @(*)  
      to automatically include all inputs.

2. **Blocking vs Non-blocking Assignments**

    - **Blocking (`=`):** Executes statements sequentially, line-by-line.

    - **Non-blocking (`<=`):** Executes all statements in parallel, crucial for sequential logic to preserve correct data dependencies.

    - Using blocking assignments incorrectly in sequential blocks can cause data to overwrite prematurely, leading to functional mismatches.

3. **Non-standard Verilog Constructs**

    - Some code styles or constructs may not synthesize as expected or may behave differently in simulators.

---

## 🛠️ Lab Activities: Investigating Mismatches

Here we well be evaluating the designs by  
 - simulating   
 - synthesising  
 - simulating with netlist code (formal verification)

### 1. Missing Sensitivity List

- Tested with `ternary_operator_mux.v`:

- Code Analysis when using `always @(*)`.

- Tested with `bad_mux.v`:

- Waveforms differed across simulation stages due to incomplete sensitivity list (`always @(sel)`).

## Results 

ⅰ. Ternary Operator Mux =

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/ternary_op_sim.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/ternary_op_mux_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/ternary_op_net_sim.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

ⅱ. Bad Mux =

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/bad_mux_sim1.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/bad_mux_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/bad_mux_sim2.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

### 2. Blocking vs Non-blocking Assignments

- Experiments done on blocking caveat design revealed how the use of blocking versus non-blocking assignments impacted the simulation results, especially in sequential parts of the design.

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/blocking_caveat_sim1.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/blocking_caveat_sch.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>
<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_4/images/blocking_caveat_sim2.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

---

## 📌 Summary

- GLS is essential to validate the **correctness of synthesized gate-level netlists**, ensuring no functional regressions.

- Mismatches often arise from **coding mistakes** such as incomplete sensitivity lists and wrong use of blocking assignments.

- Writing synthesizable, simulation-consistent RTL is critical for robust design and verification workflows.

---


