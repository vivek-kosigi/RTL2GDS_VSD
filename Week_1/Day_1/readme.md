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

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_1/simulation_block_diagram.png" 
       alt="Simulation Block Diagram" width="600"/>
</p>

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

### Multiplexer Design code (`good_mux.v`)
```verilog
module good_mux (input i0, input i1, input sel, output reg y);
always @(*)
begin
    if(sel)
        y <= i1;
    else
        y <= i0;
end
endmodule
```

**My Understanding of How It Works:**
- **Inputs:** `i0`, `i1` (data inputs), `sel` (select line)
- **Output:** `y` (registered output)
- **Logic:** When `sel` is 1, `y` gets `i1`; when `sel` is 0, `y` gets `i0`

### Testbench code (`tb_good_mux.v`)

```verilog
`timescale 1ns / 1ps
module tb_good_mux;
        // Inputs
        reg i0,i1,sel;
        // Outputs
        wire y;

        // Instantiate the Unit Under Test (UUT)
        good_mux uut (
                .sel(sel),
                .i0(i0),
                .i1(i1),
                .y(y)
        );

        initial begin
        $dumpfile("tb_good_mux.vcd");
        $dumpvars(0,tb_good_mux);
        // Initialize Inputs
        sel = 0;
        i0 = 0;
        i1 = 0;
        #300 $finish
            end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

I analyzed how the testbench instantiates the multiplexer and applies test vectors:
- `sel` toggles every 75 time units
- `i0` toggles every 10 time units  
- `i1` toggles every 55 time units
- My simulation ran for 300 time units

---

## My Simulation Results
I captured my simulation waveform and saved it as `simulated_wavefrom.png`. The waveform clearly showed:
- The select signal `sel` toggling every 75 time units
- Input `i0` toggling every 10 time units  
- Input `i1` toggling every 55 time units
- Output `y` correctly following the multiplexer logic

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_1/simulated_wavefrom.png" 
       alt="Simulated Wavefrom of MUX" width="600"/>
</p>

---

## 🏗️ What is Synthesis?

**Synthesis** is the process of **converting RTL (behavioral Verilog) into a gate-level netlist**—a format interpretable for chip fabrication. The *synthesizer* tool handles this translation.

- **Synthesizer Tool:** [`Yosys`](https://yosyshq.net/yosys/)
- **Inputs needed:**
    - Design (`.v` file)
    - Library (`.lib` file)
    - (Optionally) Constraints (`.sdc` file)
- **Output:** Technology-mapped netlist (`netlist.v`)

<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_1/synthesis_block_diagram.png" 
       alt="Synthesis Block Diagram" width="600"/>
</p>

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


<p align="center">
  <img src="https://github.com/vivek-kosigi/RTL2GDS_VSD/blob/main/Week_1/Day_1/synthesised_schematic.png" 
       alt="Synthesised Diagram" width="600"/>
</p>

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

