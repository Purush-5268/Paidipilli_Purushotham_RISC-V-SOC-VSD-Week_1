# 🌟 Day 1: RTL Design & Synthesis with Verilog

👋 Welcome to **Day 1 of my RTL Workshop Journey!**
Today marks the first step into the exciting world of **Digital Design**. We’ll explore **Verilog HDL**, open-source simulation with **Icarus Verilog (iverilog)**, and logic synthesis using **Yosys**.

This day is all about building a **strong foundation** with hands-on labs, clear concepts, and powerful tools. Let’s dive in! ⚡

---

## 📑 Table of Contents

1. 🎯 [Simulator, Design & Testbench Basics](#-simulator-design--testbench-basics)
2. ⚙️ [Getting Started with Icarus Verilog (iverilog)](#️-getting-started-with-icarus-verilog-iverilog)
3. 🔬 [Lab 1: Simulating a 2-to-1 Multiplexer](#-lab-1-simulating-a-2-to-1-multiplexer)
4. 📝 [Verilog Code Deep Dive](#-verilog-code-deep-dive)
5. 🏗 [Introduction to Yosys & Gate Libraries](#-introduction-to-yosys--gate-libraries)
6. 🧩 [Synthesis Lab with Yosys](#-synthesis-lab-with-yosys)
7. 🏁 [Key Takeaways](#-key-takeaways)

---

## 🎯 Simulator, Design & Testbench Basics

🔹 **Simulator** → Software that verifies your circuit’s behavior before real hardware.
🔹 **Design** → The Verilog code you write to describe logic.
🔹 **Testbench** → A "playground" that applies test inputs to the design and checks outputs.

💡 Think of it like this:

* **Design = Engine*Perfect 🚀 Thanks for sharing the reference.
I’ll now reframe this into a **more attractive, innovative, and professional Day 1 README style**.
I’ll use ✅ emojis, callouts, modern formatting, and storytelling so it feels more engaging and less like plain notes.

Here’s a polished version:

---
*
* **Testbench = Driver**
* **Simulator = Race Track**

---

## ⚙️ Getting Started with Icarus Verilog (iverilog)

**Icarus Verilog (iverilog)** is an open-source simulator for Verilog.

🔄 **Flow of Simulation:**

1. Feed both design + testbench to `iverilog`
2. Run simulation → Generates `.vcd` file
3. View results in **GTKWave** 🎛

---

## 🔬 Lab 1: Simulating a 2-to-1 Multiplexer

👉 Let’s simulate a simple **MUX (2:1)**

### 🛠 Setup

```bash
# Clone the repo
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files

# Install toolsPerfect 🚀 Thanks for sharing the reference.
I’ll now reframe this into a **more attractive, innovative, and professional Day 1 README style**.
I’ll use ✅ emojis, callouts, modern formatting, and storytelling so it feels more engaging and less like plain notes.

Here’s a polished version:

---

sudo apt install iverilog
sudo apt install gtkwave
```

### ▶️ Run Simulation

```bash
# Compile
iverilog good_mux.v tb_good_mux.v

# Run
./a.out

# View waveform
gtkwave tb_good_mux.vcd
```

✅ Output: A clean waveform in GTKWave

---

## 📝 Verilog Code Deep Dive

Here’s the **2:1 MUX** in Verilog:

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
always @ (*)
begin
    if(sel)
        y <= i1;Perfect 🚀 Thanks for sharing the reference.
I’ll now reframe this into a **more attractive, innovative, and professional Day 1 README style**.
I’ll use ✅ emojis, callouts, modern formatting, and storytelling so it feels more engaging and less like plain notes.

Here’s a polished version:

---

    else 
        y <= i0;
end
endmodule
```

📌 **Logic:**

* If `sel = 1` → `y = i1`
* If `sel = 0` → `y = i0`

---

## 🏗 Introduction to Yosys & Gate Libraries

💡 **Yosys** = Open-source tool that converts **Verilog** into a **gate-level netlist**.

✨ **Why it’s powerful:**

* Converts HDL → logic circuit
* Optimizes design (area, power, speed)
* Maps logic to real hardware cells
* Verifies correctness

🗂 **Gate Libraries (.lib):** Contain **different flavors** of gates (AND, OR, NOT, etc.) with:

* ⏱ Speed (fast vs slow)
* 🔋 Power (low-power gates)
* 📏 Area (compact cells)
* 💪 Drive strength (stronger output drive)

---

## 🧩 Synthesis Lab with Yosys

Step-by-step flow:

```bash
# Launch yosys
yosys

# Load library
read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib

# Load design
read_verilog good_mux.v

# Synthesize
synth -top good_mux

# Technology mapping
abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib

# Visualize netlist
show
```

📌 Output → Gate-level schematic of the MUX 🎨

---

## 🏁 Key Takeaways

✅ Understood **simulator, design & testbench** roles
✅ Simulated a **2:1 multiplexer** using iverilog & GTKWave
✅ Analyzed Verilog code deeply
✅ Learned **Yosys synthesis flow**
✅ Explored **gate libraries & flavors**

🚀 **Day 1 = Solid foundation for RTL design & synthesis!**

---

Would you like me to also **design a neat banner-style header (ASCII or markdown-art)** for the repo to make it stand out when people open it on GitHub?
