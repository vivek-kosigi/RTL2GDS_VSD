# 🧠 VSD - Static Timing Analysis (STA) – I

Static Timing Analysis (STA) is a key process in VLSI design used to verify whether a circuit meets timing requirements **without simulation**.  
This course explains STA from the **path-level** to **transistor-level**, covering setup/hold checks, variations, and pessimism removal.

---

## ⚙️ 1. Fundamentals of Timing Analysis

### 🔹 Timing Path & Arrival Path
- A **timing path** connects a startpoint (launch flop/input) to an endpoint (capture flop/output).
- It consists of:
  - **Launch Clock Path** → when clock triggers source flop.
  - **Data Path** → combinational logic between flops.
  - **Capture Clock Path** → when clock reaches destination flop.
- **Arrival Path / AAT** = time when data actually arrives at endpoint.

### 🔹 Required Time & Slack
- **Required Arrival Time (RAT):** when data *must* arrive to meet setup/hold.
- **Slack = RAT - AAT**
  - Positive → timing met  
  - Zero → critical path  
  - Negative → violation

### 🔹 Setup and Hold Checks
- **Setup time:** data must be stable *before* clock edge.
- **Hold time:** data must stay stable *after* clock edge.
- Violations:
  - Late data → setup violation  
  - Early data → hold violation

### 🔹 Data Check & Latch Timing
- **Data checks:** for asynchronous or non-flop paths.
- **Latch timing:** latches are level-sensitive → allow **time borrowing**.

### 🔹 Slew, Load & Clock Checks
- **Slew:** rate of signal transition; slow slews increase delay.
- **Load:** output capacitance a gate drives.
- **Clock checks:** skew, jitter, uncertainty, duty cycle → affect timing margin.

---

## 🧮 2. Timing Graph & Path Computations

### 🔹 Logic → Timing Graph
- Circuit modeled as a **graph**:
  - **Nodes:** pins/nets  
  - **Edges:** delays

### 🔹 Actual Arrival Time (AAT)
- Time data **actually reaches** a node.
- `AAT = Clock Launch + Clk→Q + Data Path Delay`

### 🔹 Required Arrival Time (RAT)
- Latest (for setup) or earliest (for hold) time data **can arrive**.

### 🔹 Slack and GBA–PBA
- **Slack = RAT - AAT**
- **GBA (Graph-Based Analysis):** fast, conservative (pessimistic)
- **PBA (Path-Based Analysis):** slower, detailed, less pessimistic

### 🔹 Pins to Nodes Conversion
- Each pin becomes a node for fine-grained AAT/RAT/Slack calculation.
- STA tools traverse graph topologically to find **critical paths**.

---

## 🔬 3. Transistor-Level & Library Characterization

### 🔹 Flip-Flop Circuit Basics
- Flip-flops are built from CMOS inverters & transmission gates.
- Timing parameters extracted from transistor-level behavior:
  - Setup, Hold, and Clock-to-Q delay.

### 🔹 Positive & Negative Latch Operation
- **Positive latch:** transparent when clock = 1.  
- **Negative latch:** transparent when clock = 0.  
- Used for **time borrowing** in latch-based designs.

### 🔹 Setup Time Characterization
- Measured as **minimum stable time** before clock edge for correct data capture.
- Extracted and stored in `.lib` timing library.

### 🔹 Clock-to-Q (Clk→Q) Delay
- Time between clock edge and output change.
- Affects data launch timing and AAT.

### 🔹 Eye Diagram & Jitter
- **Eye diagram:** visual clock quality test.
- **Jitter:** deviation of clock edges from ideal timing.
- STA adds **clock uncertainty = jitter + skew** to setup time checks.

---

## ⏱️ 4. Setup & Hold Analysis Representation

### 🔹 Setup Analysis
- Focuses on **maximum delay paths**.
- Determines **maximum frequency** of the design.

### 🔹 Hold Analysis
- Focuses on **minimum delay paths**.
- Ensures data stability immediately after clock edge.

### 🔹 Graphical & Textual Reports
- Graphs show timing path relationships.
- Reports show:
```txt
Startpoint: FF1/Q
Endpoint: FF2/D
Data Arrival Time = ...
Required Time = ...
Slack = ...
```
- Tools: **PrimeTime**, **Tempus**, **OpenTimer**, etc.

---

## 🌡️ 5. Sources of Variation

### 🔹 Etching Variation
- Variations in metal width/spacing alter resistance (R) and capacitance (C).
- Changes signal propagation delay.

### 🔹 Oxide Thickness Variation
- Affects transistor **threshold voltage** & **drive strength**.
- Leads to delay mismatch across devices.

### 🔹 Relationship: Resistance, Drain Current, Delay
- Delay ∝ R × C  
- Resistance ∝ 1/Id  
- Higher drain current → lower delay.  
- Used for PVT (Process, Voltage, Temperature) corner modeling.

---

## 📈 6. OCV & Pessimism Removal

### 🔹 On-Chip Variation (OCV)
- Local process variations cause launch & capture paths to behave differently.
- STA uses **derating factors** to model slow/fast corners.

### 🔹 Setup Timing with OCV
- Analyzes **worst-case slow data + fast clock** to ensure setup margin.

### 🔹 Hold Timing with OCV
- Analyzes **fast data + slow clock** to prevent hold violations.

### 🔹 Common Path Pessimism Removal (CPPR)
- Removes overly pessimistic assumptions when launch & capture share same clock segments.
- Makes slack results **more accurate and realistic**.

---

## 🏁 Conclusion

The course builds a strong foundation in **Static Timing Analysis** by connecting:
- **Path-level timing (AAT, RAT, Slack)**  
- **Circuit-level behavior (flops, latches, jitter)**  
- **Variation-aware checks (OCV, CPPR)**  

By mastering these, an engineer can:
- Predict and fix timing violations early,  
- Optimize setup/hold margins,  
- Ensure reliable silicon performance **before tape-out**.

---
