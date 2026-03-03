# Day 2: Timing Libraries, Synthesis Approaches, and Efficient Flip-Flop Coding 🚀

Welcome to **Day 2 of the RTL Workshop**!
This session dives into three essential concepts for RTL design:

* 📂 Understanding **timing libraries** (`.lib`) in the SKY130 PDK
* 🏗️ Comparing **Hierarchical vs. Flat synthesis** techniques
* ⚡ Exploring **efficient coding styles for flip-flops**

---

## 📖 Contents

1. [Timing Libraries](#-timing-libraries)

   * SKY130 PDK Overview
   * Decoding `tt_025C_1v80`
   * Opening and Exploring the `.lib` File

2. [Synthesis Approaches](#-synthesis-approaches)

   * Hierarchical Synthesis
   * Flattened Synthesis
   * Key Differences

3. [Flip-Flop Coding Styles](#-flip-flop-coding-styles)

   * Asynchronous Reset D Flip-Flop
   * Asynchronous Set D Flip-Flop
   * Synchronous Reset D Flip-Flop

4. [Simulation & Synthesis Workflow](#-simulation--synthesis-workflow)

   * Icarus Verilog Simulation
   * Synthesis with Yosys

---

## ⏱️ Timing Libraries

### SKY130 PDK Overview

The **SKY130 PDK** is an **open-source Process Design Kit** based on SkyWater’s 130nm CMOS technology.
It includes models and libraries describing **timing, power, and process variation**.

### Decoding `tt_025C_1v80`

* **tt** → Typical process corner
* **025C** → Temperature: 25 °C
* **1v80** → Core voltage: 1.8 V

👉 This naming tells us the **exact conditions** modeled in the library.

### Opening the `.lib` File

```bash
sudo apt install gedit
gedit sky130_fd_sc_hd__tt_025C_1v80.lib
```
---

## 🏗️ Synthesis Approaches

### Hierarchical Synthesis

* Preserves module boundaries
* Faster synthesis for large designs
* Easier debugging & modular flow
* **Limitation**: fewer cross-module optimizations

### Flattened Synthesis

* Flattens all modules into a single netlist
* Allows whole-design optimizations
* **Limitation**: harder debugging & higher runtime

📸 <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/7f047672-3221-4bf4-90ec-9b5eca1134e3" />

### Key Differences

| Aspect             | Hierarchical 🧩        | Flattened 🗜️          |
| ------------------ | ---------------------- | ---------------------- |
| **Hierarchy**      | Preserved              | Collapsed              |
| **Optimization**   | Module-level           | Whole-design           |
| **Runtime**        | Faster (large designs) | Slower (large designs) |
| **Debugging**      | Easier                 | Harder                 |
| **Output Netlist** | Modular                | Single flat netlist    |

---

## ⚡ Flip-Flop Coding Styles

### 🔹 Asynchronous Reset DFF

```verilog
module dff_asyncres (input clk, input async_reset, input d, output reg q);
  always @ (posedge clk, posedge async_reset)
    if (async_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```

### 🔹 Asynchronous Set DFF

```verilog
module dff_async_set (input clk, input async_set, input d, output reg q);
  always @ (posedge clk, posedge async_set)
    if (async_set)
      q <= 1'b1;
    else
      q <= d;
endmodule
```

### 🔹 Synchronous Reset DFF

```verilog
module dff_syncres (input clk, input sync_reset, input d, output reg q);
  always @ (posedge clk)
    if (sync_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```
---

## 🖥️ Simulation & Synthesis Workflow

### Icarus Verilog (Simulation)

```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

📸 <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/9ca3996b-451a-461e-902d-4a6e2a599523" />

### Yosys (Synthesis)

```tcl
yosys
read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog dff_asyncres_netlist.v
```

📸 <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/ab93db43-f6ef-48fb-9c62-87cff9be3c06" />

---

## ✅ Summary

On **Day 2**, we:

* Understood how **timing libraries** define PVT conditions
* Compared **Hierarchical vs. Flattened synthesis** flows
* Learned **efficient flip-flop coding styles**
* Practiced **simulation & synthesis** using Icarus + Yosys

👉 These skills build the foundation for RTL-to-GDSII flows in open-source VLSI design.






