# Hardware Prototyping & Custom Interconnect Extension of ARM Cortex-M3 SoC

A customized, fully synthesizable System-on-Chip (SoC) architecture built around an **ARM Cortex-M3 32-bit RISC processor core** coupled with an IoT compute subsystem. This project involved migrating the architecture from an Intel platform over to a **Xilinx Artix-7 FPGA**, addressing peripheral connectivity constraints by expanding the underlying bus matrix infrastructure.

---

## 📊 FPGA Implementation & Performance Metrics

The SoC was synthesized and implemented for the **Artix-7 FPGA platform**. The following resource utilization and power figures are extracted from Xilinx Vivado implementation reports.

### 1. Power Analysis Breakdown (Vivado Implemented Netlist)
*   **Total On-Chip Power:** 0.368W
*   **Dynamic Circuit Power:** 0.265W (72%)
*   **Device Static Power:** 0.103W (28%)

### 2. Device Resource Utilization (Artix-7 XC7A100T)
*   **Look-Up Tables (LUTs):** 25,397 / 63,400 (**40.06% Utilization**)
    *   *LUT as Logic:* 24,482
    *   *LUT as Memory:* 915
    *   *LUT as Distributed RAM:* 152
    *   *LUT as Shift Register:* 763
*   **Flip-Flops:** 14,071 / 126,800 (**11.10% Utilization**)
*   **F7 Muxes:** 145
*   **F8 Muxes:** 19

---

## ⚡ Hardware Customization & Interconnect Engineering

The primary architectural modification addressed peripheral connectivity limitations by expanding the existing AMBA bus infrastructure.

### 1. AMBA Interconnect Expansion (18-Master / 18-Slave Port Topology)
*   **Bus Expansion:** Modified the AMBA Advanced High-performance Bus (AHB-Lite) and Advanced Peripheral Bus (APB) interconnect matrices, expanding the architecture from an 8-port baseline to support **18 master and 18 slave ports,** significantly increasing peripheral connectivity.
*   **Address Decoding:** Implemented 32-bit address decoding logic for the AHB interconnect. Customized APB decoding logic uses address-bit selection to distinguish peripheral access regions.

### 2. Memory Subsystem Expansion
*   **SRAM Subsystem:** Expanded the on-chip SRAM capacity to **128 KB**, implemented using FPGA block RAM resources.
*   **Primary Flash:** Expanded non-volatile code memory space from **256KB to 512KB** to accommodate larger firmware images.

### 3. FPGA Clock Tree Restructuring
*   Integrated an on-chip **Mixed-Mode Clock Manager (MMCM)** to generate the required internal system clocks from the Artix-7 board's onboard oscillator.

---

## 🛠️ Toolchain Workflow & Execution

The hardware-software co-design flow combines RTL simulation with FPGA-based hardware execution:

1.  **Software Compilation:** Developed embedded C applications and compiled them using **Keil µVision5** to generate firmware binaries.
2.  **RTL Simulation:** Simulated the Verilog RTL and customized interconnect logic using **Xilinx Vivado** to verify design functionality.
3.  **FPGA Implementation and Deployment:** Synthesized and implemented the modified ARM Cortex-M3 SoC using Xilinx Vivado and generated the FPGA .bit bitstream file. Programmed the Artix-7 FPGA board with the hardware design, loaded the compiled application code into the SoC's Flash memory, and executed the firmware on the ARM Cortex-M3 processor following CPU reset.

---

## 📂 Repository Layout & Project Artifacts

All project blueprints, FPGA implementation and verification artifacts, and implementation toolchain reports are included in the repository for reference:

*   `Cortex-M3 Design with IOT subsystem.jpg` — Baseline architectural block schematic showing the integrated processor and bus infrastructure.
*   `Modified Interconnect Platform.jpg` — Modified architecture illustrating the expanded interconnect and custom address-decoding logic.
*   `lut_report.jpg` — Vivado resource utilization report for the Artix-7 FPGA.
*   `power_report.jpg` — Vivado power analysis report showing dynamic, static, and total estimated on-chip power.
*   `Screenoutput.jpg` — Hardware execution terminal capture showing runtime output and memory code-loading activity.
*   `README.md` — Project documentation and technical overview.
---

## 📜 Citation & Publication Details
This SoC design and FPGA implementation are documented in the following publication:
*   **Trisha Maddanna**, Vaishnavi U, Gahan A V, *"Hardware Implementation of ARM Cortex-M3 Design on FPGA,"* **International Educational Applied Scientific Research Journal (IEASRJ)**, Vol. 9, No. 12, 2024.
