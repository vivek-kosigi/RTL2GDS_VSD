# Week 2 Task 1  
# 📘 SoC Design Fundamentals & VSDBabySoC  

## 🔹 What is an SoC?  
A **System-on-Chip (SoC)** is an integrated circuit that combines all the essential components of a complete computing system on a single chip.  
It typically includes:  
- CPU  
- GPU  
- Memory  
- DSP  
- Power management  
- Peripherals (UART, WiFi, Bluetooth, Timers, etc.)  

👉 Found in almost every electronic device today: **smartphones, laptops, smartwatches, IoT devices, medical equipment, and vehicles.**  

### ✅ Why SoC?  
- **Space Saving** 🧩 – all components on one chip → portable design  
- **Energy Efficient** ⚡ – shorter interconnects reduce power loss  
- **High Performance** 🚀 – faster communication between blocks  
- **Cost Effective** 💰 – cheaper than assembling multiple chips  

---

## 🖥️ Main Components of an SoC  
1. **CPU (Central Processing Unit)** – The brain; handles instructions & computations.  
2. **GPU (Graphics Processing Unit)** – Enhances visual quality, rendering images/videos.  
3. **Memory (ROM, RAM)** – Stores data for quick access.  
4. **DSP (Digital Signal Processor)** – Specialized for audio, video, and signal processing.  
5. **Power Management** – Distributes stable power across the chip.  
6. **Peripherals** – Interfaces for communication: I/O, WiFi, Bluetooth, etc.  

---

## 🌍 SoCs in the Real World  
- **Smartphones & Tablets** 📱  
- **Smartwatches & Wearables** ⌚  
- **Computers & Laptops** 💻  
- **IoT Devices & Vehicles** 🚗  
- **Medical Equipment** 🏥  

### 🔥 Famous SoCs  
- **Qualcomm Snapdragon**  
- **Samsung Exynos**  
- **Apple A-series**  
- **Google Tensor**  
- **NVIDIA Tegra**  

---

## ⚠️ Challenges in SoC Design  
- **Complexity** – integrating multiple components with timing & power constraints  
- **Heating Issues** – high density of circuits → power dissipation  
- **Flexibility** – limited ability to modify once fabricated  

---

## 🧩 Types of SoCs  
### 1. **Microcontroller-based SoC**  
- Low power, used for simple tasks (cars, sensors, remotes).  
- Examples: **ESP8266/ESP32, STM32, PIC32**  

### 2. **Microprocessor-based SoC**  
- High performance, used in consumer electronics (TVs, smartphones).  
- Examples: **Snapdragon, Apple A16, Exynos**  

### 3. **Application-Specific SoC (ASIC-based)**  
- Designed for dedicated tasks (AI accelerators, GPUs).  
- Examples: **NVIDIA Tegra, Google TPU, ASICs in trading systems**  

---

# 🍼 VSDBabySoC – Learning SoC with RISC-V  

The **VSDBabySoC** is a compact educational SoC built on **RISC-V architecture** with open-source IP cores.  
It’s designed to help learners explore **Digital, Analog, and Mixed-Signal (DAC)** domains together, covering the full flow from **RTL to GDS**.  

### ⚙️ Main Components  
1. **RVMYTH (RISC-V CPU)** 🧠 – a simple CPU core for processing & communication  
2. **PLL (Phase-Locked Loop)** ⏱️ – generates stable clocks for CPU & DAC  
3. **DAC (Digital-to-Analog Converter)** 🎵 – converts digital output into analog signals (audio/video)  

---

## 🔄 PLL (Phase-Locked Loop)  
- Contains **Phase Detector, Loop Filter, VCO**  
- Ensures stable clocking and avoids delays from external clocks  

---

## 🎚️ DAC (Digital-to-Analog Converter)  
- Converts binary digital values into continuous analog output  
- Common Types:  
  - **Weighted Resistor DAC**  
  - **R-2R Ladder DAC**  

---

## 📌 Key Takeaways  
- SoCs integrate all components of a system onto a single chip → compact, efficient, and powerful  
- Widely used in **consumer electronics, automotive, IoT, and AI**  
- VSDBabySoC provides **hands-on learning** with CPU, PLL, and DAC → bridging theory with practical SoC design  

---
