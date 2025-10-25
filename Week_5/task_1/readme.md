
# 🧱 Task 1 – OpenROAD Installation and Setup

---

## 🎯 Objective
The goal of this task is to **install and configure the OpenROAD Flow Scripts (ORFS)** environment on a Linux system.  
OpenROAD provides an **end-to-end open-source flow** for **RTL-to-GDSII physical design**, including synthesis, placement, routing, STA, and signoff.

This setup establishes the foundation for performing backend tasks such as **floorplanning**, **placement**, and **timing optimization** in upcoming projects.

---

## ⚙️ About OpenROAD
OpenROAD enables a **fully automated digital design flow** for VLSI implementation.  
It integrates the following tools:

- **Yosys** – Logic Synthesis  
- **OpenROAD** – Placement, CTS, and Routing  
- **OpenSTA** – Static Timing Analysis  
- **KLayout** – Layout visualization  
- **Magic** – Layout editing and verification  

The framework is widely adopted for open-source chip design, research, and academic projects.

---

## 🪜 Installation Steps

### **1. Clone the Repository**
```txt
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
```

This downloads the main repository along with all its submodules.

---

### **2. Run the Setup Script**
```txt
sudo ./setup.sh
```

This step installs essential dependencies, including:

- `Yosys`, `OpenSTA`
- `Magic`, `KLayout`
- `CMake`, `Python` build utilities  

🕐 *Note:* This step can take some time depending on system performance.

---

### **3. Build OpenROAD Locally**
```txt
./build_openroad.sh --local
```

This compiles the OpenROAD executables from source.  
Upon completion, binaries are stored in the **build directory**.

---

### **4. Verify Installation**
Confirm successful installation by checking available commands:
```txt
source ./env.sh
yosys -help
openroad -help
```

If these commands display help text, OpenROAD and Yosys are working correctly.

---

### **5. Run the OpenROAD Flow**
```txt
cd flow
make
```

Executes a basic design flow (like `gcd` with `nangate45` library) to validate installation.

---

### **6. Launch the GUI**
```txt
make gui_final
```

This opens the **layout visualization window** displaying standard cells and floorplans.

---

## 📁 Directory Structure Overview
```txt
OpenROAD-flow-scripts/
├── docker/ → Docker setup files
├── docs/ → Documentation and usage guides
├── etc/ → Dependency scripts and config files
├── flow/ → RTL-to-GDSII automation framework
│ ├── designs/ → Example design configurations
│ ├── platform/ → Tech files, libraries, and LEFs
│ ├── Makefile → Flow automation control
├── tools/ → Utility submodules (Yosys, OpenSTA, etc.)
└── setup_env.sh → Environment initialization script
```


---

## 🔧 Alternative Manual Installation
If setup fails, dependencies can be installed manually:
```txt
sudo apt install -y libgtest-dev cmake build-essential libspdlog-dev liblemon-dev
git clone https://github.com/google/or-tools.git
cd or-tools
mkdir build && cd build
cmake -DBUILD_DEPS=ON -DCMAKE_BUILD_TYPE=Release ..
make -j$(nproc)
sudo make install

git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD.git
cd OpenROAD
sudo ./etc/DependencyInstaller.sh -base
mkdir build && cd build
cmake ..
make -j$(nproc)
```


---

## 🔍 Verification
Run these checks to ensure successful setup:
```txt
openroad -version
make gui_final
```


You should see the GUI open with no fatal build errors ✅  

---

## ⚠️ Issues Faced and Solutions

| **Issue** | **Cause** | **Fix / Solution** |
|------------|------------|---------------------|
| `KLayout failed` during setup | Missing dependency | Installed manually using `sudo apt install klayout` |
| `Permission denied` on scripts | Setup script not executable | Ran `chmod +x setup.sh` |
| Long build times | Limited CPU threads | Used `make -j$(nproc)` for parallel jobs |
| Python import errors | Missing module dependencies | Installed using `pip install -r requirements.txt` |

---

## 📊 Results
- ✅ **OpenROAD flow scripts successfully built and verified**  
- ✅ Successfully ran basic design test (`make`)  
- ✅ GUI launched without errors (`make gui_final`)  
- ✅ Environment ready for next stages – **Floorplan**, **Placement**, and **Routing**

---

