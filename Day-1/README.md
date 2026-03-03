# 🌟 Day 1: RTL Design & Synthesis

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

📂 **Simulator**

* Software that **verifies the behavior** of your digital circuit.
* It continuously **checks for changes in inputs**, and whenever inputs change, the outputs update accordingly.

📂 **Design**

* The **actual Verilog code**.
* Describes the **intended functionality** of the circuit to meet required specifications.

📂 **Testbench**

* A setup to **apply stimulus (inputs)** to the design.
* Used to verify whether outputs match expected results.

📊<img width="1108" height="442" alt="Image" src="https://github.com/user-attachments/assets/0a70940a-d265-424b-9b8b-97159efea7a8" />

---

## ⚙️ Getting Started with Icarus Verilog (iverilog)

**Icarus Verilog (iverilog)** is an open-source simulator used to compile and run Verilog code.

🔄 **Simulation Flow:**

1. Provide **design + testbench** as input to `iverilog`.
2. Run simulation → generates a **VCD (Value Change Dump)** file.
3. Open the `.vcd` file in **GTKWave** to view signal waveforms.

📊 **Icarus Verilog + GTKWave flow diagram**

<img width="918" height="389" alt="Image" src="https://github.com/user-attachments/assets/ccea1f7c-0fa0-41ad-bcac-204c3f103026" />

---

## 🔬 Lab 1: Simulating a 2-to-1 Multiplexer

👉 Let’s simulate a simple **2:1 MUX**

### 🛠 Setup

```bash
# Ensure these tools are installed , if not install these tools
sudo apt install iverilog
sudo apt install gtkwave

# Enter into root
sudo su
# Create your desired folder and enter into it 
mkdir VSD
cd VSD

# Clone the repoWould you like me to also **add a section called “🖼️ Outputs” at the end** where you can neatly place your waveform screenshot + schematic so readers see results directly without scrolling back?

git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```

### ▶️ Run Simulation

```bash
# Compile design + testbench
iverilog good_mux.v tb_good_mux.v

# Run simulation (generates VCD dump)
./a.out
```

📌 When you run `./a.out`, you’ll see:

```
VCD info: dumpfile tb_good_mux.vcd opened for output.
```

This means the **waveform dump (VCD file)** is successfully created.

Now open it in GTKWave:

```bash
gtkwave tb_good_mux.vcd
```

📊 **Output waveform**

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/ce7431c5-267b-400e-8160-1d90a343019d" />

---

## 📝 Verilog Code Deep Dive

Here’s the **2:1 MUX** in Verilog:

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
always @ (*)
begin
    if(sel)
        y <= i1;
    else 
        y <= i0;
end
endmodule
```

📌 **Logic Explanation:**

* If `sel = 1` → `y = i1`
* If `sel = 0` → `y = i0`

---

## 🏗 Introduction to Yosys & Gate Libraries

💡 **Yosys** = Open-source tool that converts **Verilog RTL → Gate-level Netlist**

✨ **Why it’s powerful:**

* Converts HDL into hardware-ready circuit
* Optimizes **speed / area / power**
* Maps logic to standard cells from library
* Generates schematics for visualization

🗂 **Gate Libraries (.lib):** Contain **different flavors** of gates with trade-offs in:

* ⏱ Speed
* 🔋 Power
* 📏 Area
* 💪 Drive strength

---

## 🧩 Synthesis Lab with Yosys

Before launching Yosys, navigate into the `cd ~/VLSI/sky130RTLDesignAndSynthesisWorkshop` directory within the cloned workshop folder.

### 🖥 Yosys Flow

```bash
# Launch yosys
yosys

# Load the technology library
# read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -lib lib/sky130_fd_sc_hd__tt_025C_1v80.lib

# Load your design
# read_verilog good_mux.v
read_verilog verilog_files/good_mux.v

# Synthesize the design
synth -top good_mux

# Technology mapping
# abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty lib/sky130_fd_sc_hd__tt_025C_1v80.lib

# Visualize the netlist
show
```
📐 **Gate-level schematic screenshot**

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/c8ce0867-bb33-4888-bcdc-847133d4de0e" />

---

### 📜 Generating the Netlist File

After visualizing the schematic, you can save the resulting gate-level netlist to a Verilog file.

✍️ **To write the netlist to `my_netlist.v`:**

```bash
# In the Yosys tool itself
write_verilog my_netlist.v
```

👀 **To quickly view the file from within Yosys:**

```bash
# This opens the file in the gvim editor
!gvim my_netlist.v
```

✨ **For a cleaner, simplified output (recommended for review):**

```bash
# The -noattr flag removes extra tool-specific attributes
write_verilog -noattr my_simplified_netlist.v
```

-----

## 🏁 Key Takeaways

✅ Understood **Simulator, Design & Testbench** clearly
✅ Learned why we run `./a.out` → to **generate VCD dump**
✅ Understood **VCD = Value Change Dump** file
✅ Ran first Verilog simulation with **iverilog + GTKWave**
✅ Simulated and verified **2:1 Multiplexer**
✅ Explored **Yosys synthesis flow** and gate libraries
✅ Generated both **waveform** and **schematic**

🚀 **Day 1 = Strong foundation built for RTL design & synthesis!**

---
