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

