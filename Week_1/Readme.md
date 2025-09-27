# 🖥️ Week 1: VSD Training – RTL Simulation & Synthesis

Welcome to **Week 1** of the VLSI System Design (VSD) training program.  
This folder contains **5 days of hands-on learning**, exploring RTL simulation, synthesis, standard cell libraries, optimizations, and gate-level verification.  


---

## 📂 Folder Structure

| Folder       | Description |
| ------------ | ----------- |
| `Day_1`      | RTL simulation, testbench creation, basic synthesis with Yosys, fast vs slow cells |
| `Day_2`      | Deep dive into `.lib` files, hierarchical vs flat synthesis, flip-flop coding styles, RTL optimizations |
| `Day_3`      | Combinational & sequential logic optimizations, constant propagation, retiming, state reduction, cloning |
| `Day_4`      | Gate-Level Simulation (GLS), synthesis-simulation mismatch analysis, best RTL coding practices |
| `Day_5`      | **To be added** |

---

## 📘 Day-wise Summary

### 🚀 [Day 1: RTL Simulation & Synthesis](./Day_1)
- Learned **RTL simulation** with `iverilog` + `GTKWave`  
- Created **design (`good_mux.v`)** and **testbench (`tb_good_mux.v`)**  
- Performed **synthesis with Yosys**, understanding netlist generation  
- Explored **.lib standard cells** and **fast vs slow cells**  
- Verified post-synthesis functionality

### 📚 [Day 2: .lib Files, Hierarchy, Flip-Flops & RTL Optimizations](./Day_2)
- Explored **.lib files** and PVT corners for robust design  
- Compared **hierarchical vs flat synthesis** in Yosys  
- Implemented **different flip-flop coding styles** (async/sync reset)  
- Learned RTL **optimization tricks** like power-of-two multiplication → shift-left

### 🌟 [Day 3: Combinational & Sequential Optimizations](./Day_3)
- Applied **constant propagation** and **Boolean simplification** in combinational circuits  
- Optimized sequential logic: **state reduction, retiming, cloning**  
- Ran labs (`opt_check*`, `diff_const*`, `counter_opt*`) to observe real hardware optimizations  
- Understood **unused port pruning** and area/power reduction

### 🛠️ [Day 4: Gate-Level Simulation (GLS) & Synthesis-Simulation Mismatches](./Day_4)
- Performed **GLS using netlist.v** and testbench with `.lib` files  
- Investigated common causes of simulation-synthesis mismatches:
  - Incomplete sensitivity lists (`always @(sel)` vs `always @(*)`)  
  - Blocking (`=`) vs non-blocking (`<=`) assignment misuse  
  - Non-standard Verilog constructs  
- Ran labs on muxes and sequential designs to verify correct functionality  
- Learned best practices for **synthesizable, simulation-consistent RTL**

---

## ⚙️ Tools Used

| Tool          | Purpose |
| ------------- | ------- |
| `iverilog`    | RTL simulation |
| `GTKWave`     | Waveform viewing |
| `Yosys`       | RTL synthesis and netlist generation |
| `.lib` files  | Standard cell definitions and PVT info |
| `.sdc` files  | Constraints for synthesis optimization |

---

## ✅ Key Takeaways

1. **Simulation first:** Always verify RTL functionality before synthesis.  
2. **Synthesis preserves functionality:** Map RTL to standard cells carefully.  
3. **Fast vs slow cells:** Understand trade-offs between speed, area, and power.  
4. **Hierarchical design:** Easier to debug and maintain complex designs.  
5. **GLS verification:** Ensure netlist matches RTL; watch for sensitivity list & assignment issues.  

---

*Next step:* Day 5 will cover advanced synthesis techniques, timing analysis, and hands-on labs with complex modules.
