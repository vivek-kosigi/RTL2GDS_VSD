# 🚀 Day 1: RTL Simulation & Synthesis Lab

Welcome to the beginner-friendly guide for simulating and synthesizing RTL (Register Transfer Level) digital designs. The steps, explanations, and commands here make it easy for newcomers to use open-source EDA tools, debug hardware code, and understand the purpose of each tool in the design flow.

---

## 🎯 What is Simulation?

Simulation allows hardware designers to **verify and visualize circuit functionality before fabrication**. Signals inside the design are displayed as waveforms—making it clear how the circuit responds to different input values.

- **Simulator Tool:** [`iverilog`](https://bleyer.org/icarus/)
- **Waveform Viewer:** [`GTKWave`](http://gtkwave.sourceforge.net/)

Simulation involves two main code files:
- **Design File:** Implements hardware logic (e.g., `good_mux.v`)
- **Testbench File:** Applies stimuli (test vectors) to the design (e.g., `tb_good_mux.v`)

---

## 🗂️ Cloning the Training Repository

1. **Clone the repository from GitHub:**
    ```
    git clone <repository_url>
    cd sky180RTLDesignAndSynthesisWorkshop
    ```
2. **Navigate folders:**
   - `lib/` contains standard cell libraries (e.g., `sky180_fd_sc_hd__tt_025C_1v80.lib`)
   - `verilog_files/` contains example Verilog codes and testbenches

---

## ▶️ Running the Simulation

**Step 1: Compile design and testbench**  
```
iverilog good_mux.v tb_good_mux.v
```

**Step 2: Run simulation to create waveform dump (.vcd)**  
```
./a.out
```

**Step 3: View waves using GTKWave**  
```
gtkwave tb_good_mux.vcd
```



Command to open both design and testbench files for debugging:
> ```
> vim tb_good_mux.v -o good_mux.v
> ```

---

## 🏗️ What is Synthesis?

**Synthesis** is the process of **converting RTL (behavioral Verilog) into a gate-level netlist**—a format interpretable for chip fabrication. The *synthesizer* tool handles this translation.

- **Synthesizer Tool:** [`Yosys`](https://yosyshq.net/yosys/)
- **Inputs needed:**
    - Design (`.v` file)
    - Library (`.lib` file)
    - (Optionally) Constraints (`.sdc` file)
- **Output:** Technology-mapped netlist (`netlist.v`)

---

## 📦 The `.lib` Standard Cell Library

A `.lib` file contains:
- Definitions of digital cells (AND, OR, XOR, FF, etc.)
- Timing info for different *process-voltage-temperature (PVT)* corners (slow, typical, fast)
- Power and area estimates
- Setup/hold times for reliable operation

### Why Different Cell Speeds?

- **Fast Cells:** Allow a design to run at a higher frequency (shorter delay); need for tight setup times. Consumes more power & area.
- **Slow Cells:** Useful for meeting hold time (prevents signals from racing ahead); saves power & area, but increases delay.
- **Typical Use:** Designers select a mix based on required performance & constraints.

---

## 📝 Synthesis Flow (Yosys Examples)

**1. Read the library file**  
```shell
read_liberty -lib ../lib/sky180_fd_sc_hd__tt_025C_1v80.lib
```

**2. Read your Verilog RTL code**  
```shell
read_verilog good_mux.v
```

**3. Synthesize with a defined top module**  
```shell
synth -top good_mux
```

**4. Map logic to standard cells (technology mapping)**  
```shell
abc -liberty ../lib/sky180_fd_sc_hd__tt_025C_1v80.lib
```

**5. Visualize the resulting netlist**  
```shell
show
```

**6. Write final netlist after synthesis**  
```shell
write_verilog good_mux_netlist.v  
write_verilog -noattr good_mux_netlist.v # cleaner netlist
```


---

## 🔂 Post-Synthesis Verification

Just like RTL, **simulate the synthesized netlist** to ensure nothing broke during mapping.
```
iverilog  good_mux_netlist.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

> If the waveforms match those from the RTL simulation, synthesis preserved functional correctness.

---

## ⚖️ Fast vs Slow Cells: Key Trade-offs

| Cell Type   | How It’s Built     | What It’s For             | Pros          | Cons              |
| ----------- | ----------------- | ------------------------- | ------------- | ----------------- |
| Fast Cell   | Wider transistors | Fast logic, meets setup   | Speed         | More area, power  |
| Slow Cell   | Narrower transistors | Eliminates races, meets hold | Lower power   | More delay        |

- **Constraints** in `.sdc` files guide synthesizer choices for cell selection.

---

## ✅ Recap & Key Concepts

- Simulation = verifies logic before hardware, using testvectors + waveform analysis
- Synthesis = compiles RTL into technology-mapped gates, referencing `.lib` data
- Fast vs Slow standard cells chosen based on setup/hold timing requirements
- Always resimulate netlists to ensure functional consistency

---

