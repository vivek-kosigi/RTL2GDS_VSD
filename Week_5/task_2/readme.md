# 🧩 Task 2 – Floorplan and Placement using OpenROAD

---

## 🎯 Objective
The goal of this task is to execute the **Floorplan** and **Placement** stages of the physical design flow using **OpenROAD Flow Scripts (ORFS)**.  
After successfully setting up OpenROAD in Task 1, this stage focuses on building the **core layout**, placing **standard cells**, and verifying results visually in the **OpenROAD GUI**.

---

## 📘 About This Task
In the physical design flow:

- **Floorplanning** defines the **die and core area**, allocates space for macros, IO pins, and power rails.  
- **Placement** arranges all **standard cells** within the core area to achieve efficient **timing**, **wirelength**, **utilization**, and **routing quality**.

These steps form the essentials for later stages such as **Clock Tree Synthesis (CTS)** and **Routing**.

---

## ⚙️ Commands Used

### **1. Run Floorplan**
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```

This launches the **floorplanning** step for the **vsdbabysoc** design using the **sky130hd** platform configuration.

---

### **2. Floorplan Error and Fix**

Initial run produced the following error:
```txt
[ERROR STA-0164] .../vsdbabysoc/lib/avsdpll.lib line 54, syntax error
Error: floorplan.tcl, 4 STA-0164
```


#### **Cause**
The issue was due to **partially commented blocks** inside the `avsdpll.lib` file.  
OpenROAD’s Liberty parser doesn’t support commented hierarchical pin definitions like:
```txt
//pin (GND#2) {
// direction : input;
// capacitance : 0.001;
//}
```


#### **Fix**
- Open *avsdpll.lib* file  
- Comment or delete the problematic block (starting at line 54)  
- Save and re-run the floorplan command  

✅ **Result:** Floorplan executed successfully after Liberty syntax correction.

---

### **3. View Floorplan in GUI**
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan
```

This command opens the **OpenROAD GUI**, displaying key layout elements like:
- Die and **core area**
- **IO pin placement**
- **Power** and **ground rings**

📸 *Add Screenshot:*  
`![Floorplan Result](images/floorplan_result.png)`

---

### **4. Run Placement**
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```

This step performs **global and detailed placement** for all standard cells defined in the netlist.

---

### **5. View Placement in GUI**
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place
```

This opens the **placement view** with:
- Legally placed cells  
- No overlaps or gaps  
- Core utilization and layout fit verification  


---

### **6. View Placement Density Heatmap**
You can visualize the cell distribution in the OpenROAD GUI:

Navigate to:
```txt
Tools → Heat Maps → Placement Density → ✓ Show numbers
```

This heatmap reveals density gradients used for congestion analysis.


---

## 📁 Deliverables
1. **Terminal Outputs**
   - Command-line logs for floorplan and placement
   - Username and environment verification  
2. **GUI Screenshots**
   - Floorplan layout  
   - Standard cell placement  
   - Placement density heatmap  
3. **Explanation**
   - Step descriptions  
   - Issues encountered and resolutions  

---

## 📈 Observations
- The **floorplan stage** defines structural design boundaries.  
- The **placement stage** optimizes standard cell locations for efficient routing and minimal wirelength.  
- Placement density insight helps detect congestion early during PD flow.  
- Fixing syntax and configuration issues improves repeatability and design robustness.  

---

