# 💧 Smart Tank System

### Arduino-Based Liquid Monitoring and ROS 2 Integration

<p align="center">
  <img src="images/project_banner.png" alt="Smart Tank System project banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-In%20Development-orange?style=for-the-badge" alt="Project Status: In Development">
  <img src="https://img.shields.io/badge/Controller-Arduino%20Uno-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino Uno">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++">
  <img src="https://img.shields.io/badge/Robotics-ROS%202-22314E?style=for-the-badge&logo=ros&logoColor=white" alt="ROS 2">
</p>

<p align="center">
  An educational engineering project combining embedded systems, sensor measurements, liquid property calculations, and robotics software.
</p>

---

## 📌 Overview

The **Smart Tank System** is a liquid monitoring project designed to measure liquid level, mass, and temperature using an **Arduino Uno** and multiple sensors.

The system aims to process sensor readings and calculate useful parameters such as liquid volume, fill percentage, and density. Measurement data will be transmitted to a computer over **USB serial** for processing and visualization through **ROS 2**.

> 🚧 **Project status:** Initial planning and design. Hardware integration, Arduino firmware, sensor calibration, and ROS 2 functionality will be developed and validated progressively.

## 🎯 Objectives

- 📏 **Level Measurement** — Measure the distance between an ultrasonic sensor and the liquid surface.
- ⚖️ **Mass Measurement** — Measure liquid mass using a load cell and a suitable amplifier.
- 🌡️ **Temperature Monitoring** — Monitor liquid temperature within the intended operating range of 0–50°C.
- 🧮 **Volume Calculation** — Estimate liquid volume using measured level and tank geometry.
- 🧪 **Density Estimation** — Calculate liquid density using mass and volume measurements.
- 🔌 **Serial Communication** — Transmit measurement data from the Arduino to a computer over USB.
- 🤖 **ROS 2 Integration** — Develop software for data reception, processing, monitoring, and visualization.

## 🏗️ System Architecture

The proposed system consists of three main layers:

```text
┌────────────────────────────────────────┐
│               LIQUID TANK              │
│                                        │
│  Ultrasonic Sensor                     │
│  Load Cell + Amplifier                 │
│  Temperature Sensor                    │
└───────────────────┬────────────────────┘
                    │ Sensor Signals
                    ▼
┌────────────────────────────────────────┐
│               ARDUINO UNO               │
│                                        │
│  Sensor Acquisition                     │
│  Data Processing                        │
│  USB Serial Transmission                │
└───────────────────┬────────────────────┘
                    │ USB Serial
                    ▼
┌────────────────────────────────────────┐
│                ROS 2 PC                 │
│                                        │
│  Serial Data Reception                  │
│  Engineering Calculations               │
│  Monitoring and Visualization           │
└────────────────────────────────────────┘
```

_This diagram represents the planned architecture. The final implementation may change during development._

## 🔧 Hardware

| Component           | Purpose                                             |
| ------------------- | --------------------------------------------------- |
| Arduino Uno         | Main controller for sensor acquisition              |
| Ultrasonic sensor   | Liquid level measurement                            |
| Load cell           | Liquid mass measurement                             |
| Load cell amplifier | Interfaces the load cell with the Arduino           |
| Temperature sensor  | Liquid temperature measurement                      |
| Tank structure      | Holds the liquid and supports the measurement setup |

Exact component models, electrical connections, and calibration procedures will be documented as the hardware design develops.

## 💻 Software and Technologies

<p>
  <img src="https://img.shields.io/badge/Arduino%20IDE-00979D?style=flat&logo=arduino&logoColor=white" alt="Arduino IDE">
  <img src="https://img.shields.io/badge/C%2B%2B-00599C?style=flat&logo=cplusplus&logoColor=white" alt="C++">
  <img src="https://img.shields.io/badge/ROS%202-22314E?style=flat&logo=ros&logoColor=white" alt="ROS 2">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black" alt="Linux">
  <img src="https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white" alt="Git">
  <img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white" alt="GitHub">
</p>

- **Embedded development:** Arduino IDE and C++
- **Microcontroller:** Arduino Uno
- **Communication:** USB serial
- **Robotics middleware:** ROS 2
- **Development environment:** Linux
- **Version control:** Git and GitHub

## 📐 Engineering Calculations

The system is intended to derive additional parameters from calibrated sensor readings.

| Parameter       | Calculation or Method                               |
| --------------- | --------------------------------------------------- |
| Liquid level    | Tank reference height − measured surface distance   |
| Liquid volume   | Calculated from liquid level and tank geometry      |
| Fill percentage | (Liquid volume ÷ tank capacity) × 100%              |
| Liquid mass     | Calibrated load cell reading with tare compensation |
| Liquid density  | Liquid mass ÷ liquid volume                         |

The calculations will account for tank geometry, sensor placement, calibration, measurement uncertainty, and valid measurement ranges.

**Note:** Density estimation requires valid mass and volume measurements. Results may be unreliable when the measured volume is close to zero.

## 📚 Documentation

- 📄 [Project Proposal](<docs/Team 3_Project proposal.pdf>) — Project motivation, objectives, scope, and methodology.
- 📚 [Literature Review](<docs/Team 3_Literature review.pdf>) — Background research and review of existing approaches.

Additional design documents, wiring diagrams, component specifications, and experimental results will be added as development progresses.

## 🛠️ Development Roadmap

- [x] Define the initial project scope
- [x] Prepare the project proposal
- [x] Prepare the literature review
- [ ] Finalize hardware components and specifications
- [ ] Design the wiring and hardware architecture
- [ ] Implement Arduino sensor acquisition
- [ ] Calibrate and validate individual sensors
- [ ] Implement USB serial communication
- [ ] Develop ROS 2 data reception and processing
- [ ] Build monitoring and visualization tools
- [ ] Conduct system-level testing
- [ ] Document experimental results and measurement accuracy

## 📊 Testing and Validation

Testing will focus on:

- Sensor calibration and repeatability
- Liquid level and volume estimation accuracy
- Load cell accuracy and tare compensation
- Temperature measurement accuracy
- USB serial communication reliability
- Comparison of calculated values against reference measurements
- Overall system performance under different operating conditions

Experimental results will be documented here after testing begins.

## 🔮 Future Improvements

Potential extensions include:

- Live ROS 2 dashboards and data visualization
- Data logging and historical analysis
- Measurement filtering and noise reduction
- Support for different tank geometries
- Improved calibration and uncertainty analysis
- Additional monitoring and diagnostic features

## 👨‍💻 Author

**Mohamed Samer**  
Mechatronics Engineering Student

Interested in embedded systems, robotics, automation, and engineering simulation.

---

<p align="center">
  <i>Developed as an educational engineering project exploring embedded systems, instrumentation, and robotics.</i>
</p>
