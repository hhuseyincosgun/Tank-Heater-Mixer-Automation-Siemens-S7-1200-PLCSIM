# 🛢️ Tank-Heater-Mixer Automation (Siemens S7-1200 + PLCSIM)

This project is a **Tank-Heater-Mixer automation system** developed using Siemens S7-1200 series PLC and **TIA Portal with PLCSIM**. The system automatically controls the liquid level, temperature, and mixing process, and can be fully tested in a simulation environment.

![System Diagram](https://github.com/hhuseyincosgun/TANK-HEATER-MIXER-AUTOMATION/raw/main/picture_1.png)


## 🔧 Hardware and Software Used

- **PLC:** Siemens S7-1200 (example: CPU 1212C AC/DC/RLY)
- **Programming Language:** SCL (Structured Control Language)
- **Software:**
  - TIA Portal (v16 or later)
  - PLCSIM (for virtual PLC simulation)
- **Inputs/Outputs:**
  - Digital Inputs: Start/Stop buttons, level sensors
  - Digital Outputs: Valve and mixer motor control
  - Analog Input: Liquid temperature (thermometer simulation)


## 🧪 Testing with PLCSIM

This project can be fully tested using **PLCSIM** without requiring real PLC hardware. The virtual PLC can be run within TIA Portal, and system behavior can be observed. Inputs can be triggered manually to simulate sensor signals.

## 🔁 Automation Process

![System Diagram]

1. When the **Start** button is pressed, the system is activated.
2. The **filling valve** opens, and the tank starts filling with liquid.
3. Once the **upper level sensor** detects liquid, the filling process stops.
4. If the liquid temperature is **below 50°C**, the **heater and mixer** are activated.
5. The mixer ensures that the liquid is homogeneously mixed.
6. When the temperature reaches between **45-55°C**, the **drain valve** opens to discharge the tank.
7. When the **lower level sensor** no longer detects liquid, draining stops.
8. The system then returns to the beginning and waits for the next cycle.
9. Pressing the **Stop** button deactivates the system.





Tercih edilen PLC

![image](https://github.com/user-attachments/assets/b93bb49a-24a7-4574-9dcb-0557ba0f8a4a)


Rezistans termometre için bir rtd kartı alıyorum.

![image](https://github.com/user-attachments/assets/415c60ab-e0f8-437a-8cfd-2bf68756235c)

RTD kartın donanıma göre ayarlanması:

### 🌡️ RTD Connection – 3-Wire Configuration

In this project, the **Resistance Thermometer (RTD)** is connected using a **3-wire configuration (3×1.5 mm²)**, which is ideal for medium-range distances between **10 to 150 meters**.

#### 🔍 Why 3-Wire RTD is Used

- The **3-wire RTD** is a widely accepted industrial standard that helps **minimize the error caused by lead wire resistance**.
- It offers a good balance between **measurement accuracy** and **cable cost**, compared to:
  - **2-wire**: simpler but less accurate (affected more by cable resistance)
  - **4-wire**: most accurate, but more expensive and complex
- Perfect for systems where the **PLC or temperature transmitter** is located **within 150 meters** of the RTD.

### 🔢 Analog Input Configuration – Channel 0 (IW96)

In this project, we are using **Channel 0 (IW96)** of the analog input module to read temperature values.

- The connected thermal resistor is a **Pt100 RTD sensor**, commonly used in industrial temperature measurement applications.
- The signal is processed as an **analog input word (IW96)** in the PLC program.
- The RTD provides a resistance value proportional to temperature, which is interpreted by the PLC through this analog input.

> 📌 Ensure the analog input module is configured in the TIA Portal to match the sensor type (Pt100) and wiring method (e.g., 3-wire).

### 🧩 System Design Workflow – I/O Planning and Tag Definition

Before writing any PLC code, it is essential to **define all inputs and outputs** required by the system and select the hardware accordingly.

1. **I/O Analysis**  
   - Identify all necessary **digital and analog inputs/outputs** (e.g., sensors, valves, motors).
   - Determine how many input/output channels are needed.
   - This helps in selecting the appropriate **PLC model and I/O modules**.

2. **Hardware Selection**  
   - Based on the I/O requirements, choose the correct **PLC model** (e.g., Siemens S7-1200 CPU 1212C) and necessary **expansion modules** if needed.

3. **Tag Definition**  
   - After the hardware is selected, define all required **tags** in the TIA Portal project.
   - Tags should follow a **consistent naming convention** (e.g., `I_Start_Button`, `Q_Heater`, `AI_Temperature_PT100`) for clarity and maintainability.

> 🛠️ This planning phase ensures that the system is scalable, maintainable, and compatible with both the physical setup and software logic.


To ensure structured and readable PLC programming, all inputs, outputs, and internal variables are defined as **tags** in the TIA Portal.

### 📋 PLC Tag List

| Tag Name                 | Address  | Type   | Signal Type    | Description                                |
|--------------------------|----------|--------|----------------|--------------------------------------------|
| `I_Start_Button`         | I0.0     | Bool   | Digital Input  | Starts the automation process              |
| `I_Stop_Button`          | I0.1     | Bool   | Digital Input  | Stops the system                           |
| `I_Level_High`           | I0.2     | Bool   | Digital Input  | High-level sensor                          |
| `I_Level_Low`            | I0.3     | Bool   | Digital Input  | Low-level sensor                           |
| `AI_Temperature_PT100`   | IW96     | Word   | Analog Input   | Analog input from Pt100 sensor             |
| `Q_Valve_Fill`           | Q0.0     | Bool   | Digital Output | Opens the fill valve                       |
| `Q_Valve_Drain`          | Q0.1     | Bool   | Digital Output | Opens the drain valve                      |
| `Q_Motor_Mixer`          | Q0.2     | Bool   | Digital Output | Controls the mixer motor                   |
| `Q_Heater`               | Q0.3     | Bool   | Digital Output | Controls the heater                        |

![image](https://github.com/user-attachments/assets/8881ee7b-3ad4-46c2-8764-47df528713af)


#### ✅ Tagging Guidelines

- Use **meaningful and consistent names**.
- Group tags logically: inputs, outputs, internal flags, analog values.
- Make sure the tag names match across HMI and PLC program if integrated.

> 📌 All tags can be managed from the **TIA Portal's Tag Table**, where addresses, data types, and comments should be documented clearly.
