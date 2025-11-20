# TPS5450 Buck Converter Training Project

This repository contains a hands-on **PCB training project** based on the **TPS5450 non-synchronous buck converter**, originally developed for the **HKU ROBOCON TEAM** (The University of Hong Kong).

The goal of this project is to let trainees experience the **full PCB workflow**:

- Schematic design  
- PCB layout  
- PCB fabrication (ordering boards)  
- Component purchasing  
- Soldering and assembly  
- Basic testing and measurements  

Others are **welcome to use, modify, and adapt** this project under the terms of the MIT License.

---

## 📦 Repository Contents

Typical contents of this repository include:

- `altium/`  
  - `TPS5450-Template/` – Altium project template  
    - `libs/` – Altium libraries (symbols & footprints)
        - *.SchLib* – Schematic library including TPS5450 symbol
        - *.PcbLib* – PCB footprint library including TPS5450 footprint
    - `TPS5450-Template.PrjPcb` – Altium project file
    - `sch.SchDoc` – Schematic document
    - `pcb.PcbDoc` – PCB document with board outline and design rules
  - `TPS5450-TEST/` 
    - `TPS5450-TEST.PrjPcb` – Altium project file for test kit PCB
    - `sch.SchDoc` – Schematic document for test kit 
    - `pcb.PcbDoc` – PCB document for test kit
- `LICENSE` – MIT License  
- `README.md` – This file

---

## 🎯 Project Overview

Each trainee designs and builds a **TPS5450-based non-synchronous DC-DC buck converter PCB**.

The main learning objectives are:

- Understand the operation of a **non-synchronous buck converter**  
- Learn basic **TPS5450** application and feedback network design  
- Practice **Altium schematic and PCB design**  
- Experience the complete hardware flow:  
  **design → fabrication → assembly → testing**  
- Gain confidence working with real **power electronics hardware**

---

## 🔢 Output Voltage Assignment Rule

Each trainee is assigned a **unique target output voltage** based on the **last three digits** of their student ID.

Let the last three digits be **A B C** (each 0–9):

### Normal case (A ≠ 0)

- Target output voltage: **A.BC V**

Examples:

- Student ID ends with `123` → **Vout = 1.23 V**  
- Student ID ends with `457` → **Vout = 4.57 V**

### Special case (A = 0)

If the first of the last three digits is `0`, ignore this leading zero:

- Target output voltage: **B.C5 V**

Examples:

- Student ID ends with `058` → **Vout = 5.85 V**  
- Student ID ends with `032` → **Vout = 3.25 V**

### Allowed tolerance

In general, a **±2.5% error** from the assigned target output voltage is acceptable under the specified test conditions.
Since it is impossible to achieve exact voltages due to standard resistor values, the acceptable output voltage range can be calculated as:

Example:

- Target = 5.00 V  
- Acceptable range ≈ **4.88 V – 5.13 V**

Students must design the **TPS5450 feedback network** so that the measured output voltage stays within this tolerance.

---

## 🧰 Tools & Requirements

### EDA Tool

- **Altium Designer** (version as used in your lab/course)

### Provided in This Project

- Altium **starter project/template**  
- Altium **libraries** (symbols & footprints) including TPS5450  
- Main board `.PcbDoc` with:
  - Board size  
  - Layer stack / copper thickness  
  - Basic design rules  
- Test kit `.PcbDoc`:
  - Helper PCB used for:
    - Power input / output connections  
    - Load connections  
    - Convenient test points for oscilloscope probes and multimeter leads

### Recommended Self-Study

To understand what you are designing, you are encouraged to review **non-synchronous buck converters**:

- YouTube: *“Non-synchronous DC-DC Buck Converter Basics”*  
  https://www.youtube.com/watch?v=rfChSvb8FX0

- Texas Instruments: *“TPS5450 Datasheet”*  
  https://www.ti.com/lit/ds/symlink/tps5450.pdf

---

## 🧪 Student Responsibilities (Typical Flow)

This is the intended student workflow when using this project as a training exercise:

1. **Design**
   - Clone or download this repository.
   - Open the provided **Altium project template**.
   - Implement the schematic for a TPS5450-based buck converter.
   - Set the feedback network according to your **assigned output voltage**.
   - Complete the **PCB layout** following the constraints and good layout practice for switching regulators.

2. **PCB Fabrication**
   - Generate **Gerber / production files** in Altium.
   - Order PCBs from a manufacturer **on your own** (according to course or team guidelines).
   - Use the board parameters defined in the provided `.PcbDoc` unless told otherwise.

3. **Components**
   - Prepare a **BOM (Bill of Materials)**.
   - Purchase TPS5450 and all required passive components & connectors **yourself**.

4. **Assembly**
   - Solder components onto your PCB.
   - Optionally assemble the **test kit** PCB for easier testing.
   - Inspect for solder bridges, wrong orientations, missing/incorrect parts, etc.

5. **Testing**
   - Check for shorts between **VIN, VOUT, GND** before powering up.
   - Power up using a **bench power supply** with current limit.
   - Measure:
     - Output voltage and compare with your assigned target (±5%).
     - Basic load performance (under specified loads).
   - If available, use an **oscilloscope** to:
     - Observe the SW node waveform.
     - Measure output ripple.

---

## 🧪 Test Kit PCB

The repository includes a **test kit PCB** that implements a selectable resistive load bank for your converter output.

The test kit is designed as a simple, robust load for your TPS5450 board:

- It uses **five 5 Ω / 10 W cement resistors** as load elements.
- Each resistor is connected to VOUT through its own switch / control channel.
- A **5-position DIP switch** (SW1) allows you to enable **1 to 5 load resistors independently**.
- This lets you easily test how your converter behaves under **different load currents**.

For example, if your TPS5450 board outputs **5 V**:

- Each 5 Ω resistor draws approximately **1.0 A** and dissipates about **5 W**.
- Enabling 1 / 2 / 3 / 4 / 5 resistors in parallel corresponds roughly to:
  - **1 A / 2 A / 3 A / 4 A / 5 A** total load current  
    (assuming your design and test limits allow these current levels).

Since each resistor is rated at 10 W and used at around 5 W in this example, there is some power margin, but:

- The resistors will still become **very hot** at higher load settings.
- Long-duration tests at high current should be done with care and good ventilation.

Additional features:

- Indicator LEDs near each channel show which load channels are currently enabled.
- Connectors (JP1–JP4) and the large **VIN / GND / VOUT** pads make it easy to:
  - Connect a bench power supply and your TPS5450 board
  - Attach crocodile clips
  - Probe the circuit with an oscilloscope or multimeter without stressing the main PCB

---

## 🚀 How Others Can Use This Project

Even if you are **not** part of HKU ROBOCON TEAM, you can:

- Use this project as a **teaching example** for:
  - Power electronics
  - PCB design
  - Practical lab training
- Adapt the materials to your own:
  - University course
  - Student team training
  - Internal hardware bootcamp
- Modify the design to use:
  - Different output voltages  
  - Different input voltage ranges  
  - Alternative test setups

If you adapt this project, a short attribution such as the following is appreciated (but not legally required):

> Based on the TPS5450 Buck Converter Training Project by HKU ROBOCON TEAM (The University of Hong Kong).

---

## 📜 License

This project is released under the **MIT License**.

- Copyright (c) 2025 **HKU ROBOCON TEAM**

You are free to **use, copy, modify, merge, publish, distribute, sublicense, and/or sell** copies of this project, subject to the conditions in the `LICENSE` file.

See the [`LICENSE`](./LICENSE) file for full details.

---

## 🙌 Acknowledgements

- **HKU ROBOCON TEAM** – Original author and maintainer of this training project.  
- The teaching staff and mentors who contributed to:
  - Circuit design
  - PCB layout
  - Test procedures
  - Documentation

If you have questions, suggestions, or improvements, feel free to open an **issue** or submit a **pull request**.

---
