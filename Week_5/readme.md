# 🧠 Week 5 – OpenROAD Flow Setup and Implementation  

---

This week focuses on setting up the **OpenROAD Flow** environment and performing **floorplanning** and **placement** for the **vsdbabysoc** design using the **Sky130HD** technology node.  
It marks the beginning of the full **RTL-to-GDS** physical design process using open-source tools.

---

## 🧰 Task 1 – OpenROAD Installation  

### 🎯 Objective
Install and configure **OpenROAD Flow Scripts (ORFS)** on Ubuntu to enable complete automated backend flow — including synthesis, floorplan, placement, CTS, and routing.

---

### 🪜 Steps Performed

1. **Clone the Repository**
```txt
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
```

This includes all submodules required for building OpenROAD.

2. **Run the Setup Script**
```txt
sudo ./setup.sh
```

Installs dependencies such as **Yosys**, **OpenSTA**, **KLayout**, and compilers.  
*Note:* This may take several minutes.

3. **Build the Tool**
```txt
./build_openroad.sh --local
```

Compiles and generates local binaries for the OpenROAD tools.

4. **Verify Installation**
```txt
openroad -version
klayout -v
```

Both commands should output version information if the setup was successful.

5. **Troubleshooting**
- **Issue:** `KLayout` install failed  
  **Fix:** Install manually:  
  ```
  sudo apt install klayout
  ```
- **Issue:** Permission denied for `setup.sh`  
  **Fix:**  
  ```
  chmod +x setup.sh
  ```

---

### ✅ Outcome
- OpenROAD successfully installed and verified.  
- Environment ready for RTL-to-GDS tasks.  
- GUI and terminal commands functional without errors.

---

## 🧩 Task 2 – Floorplan and Placement  

### 🎯 Objective
Execute **floorplanning** and **placement** for the **vsdbabysoc** design using **Sky130HD** libraries, ensuring correct layout definition and legal placement of all standard cells.

---

### ▶ Step 1: Run Floorplan
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```

Defines:
- **Die/core area**
- **IO pin placement**
- **Power and ground ring connections**

#### ⚠ Common Error
```txt
[ERROR STA-0164] .../vsdbabysoc/lib/avsdpll.lib line 54, syntax error
Error: floorplan.tcl, 4 STA-0164
```

**Cause:** Invalid commented code block in `avsdpll.lib`.  
**Fix:** Remove or comment out the block starting at line 54 in that file.

---

### ▶ Step 2: Open Floorplan in GUI
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan
```

Visualize:
- **Core boundary and IOs**
- **Power rails and die outline**

📸 *Add screenshot later:*  
`![Floorplan Result](images/floorplan_result.png)`

---

### ▶ Step 3: Run Placement
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```

Performs global and detailed placement, optimizing for wirelength and area usage.

---

### ▶ Step 4: Open Placement in GUI
```txt
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place
```

Visualize:
- All **placed standard cells**  
- **No overlapping or unplaced instances**

📸 *Add screenshot later:*  
`![Placement Result](images/placement_result.png)`

---

### ▶ Step 5: Show Placement Density Heatmap  
In the OpenROAD GUI:
```txt
Tools → Heat Maps → Placement Density → ✓ Show numbers
```

Displays congestion and cell density for analysis.

📸 *Add screenshot later:*  
`![Placement Heatmap](images/placement_heatmap.png)`

---

## 📁 Deliverables
| Task | Deliverable | Description |
|------|--------------|-------------|
| **Task 1** | Installation Logs | Commands, outputs, and verification screenshots |
| **Task 2** | Floorplan & Placement Results | GUI screenshots, error fixes, and reports |

---

## 🧾 Summary
- Installed and verified OpenROAD on Ubuntu.  
- Completed **floorplan** and **placement** for `vsdbabysoc` using **Sky130HD**.  
- Fixed `avsdpll.lib` parser issue in Liberty file.  
- Verified design quality through layout visualization and heatmap analysis.  
- Environment ready for **CTS and Routing** in upcoming tasks.

---

