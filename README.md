# 💧 Smart Tank System

### Arduino-Based Liquid Monitoring and ROS 2 Integration

<p align="center">
  <img src="https://img.shields.io/badge/Status-In%20Development-orange?style=for-the-badge" alt="Project Status: In Development"/>
  <img src="https://img.shields.io/badge/Controller-Arduino%20Uno-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino Uno"/>
  <img src="https://img.shields.io/badge/Language-C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++"/>
  <img src="https://img.shields.io/badge/Robotics-ROS%202-22314E?style=for-the-badge&logo=ros&logoColor=white" alt="ROS 2"/>
</p>

<p align="center">
  A smart liquid tank monitoring system combining embedded systems, sensor measurements, engineering calculations, and robotics software.
</p>

---

## 📌 Overview

The **Smart Tank System** is an engineering project focused on developing a liquid tank monitoring solution using an Arduino Uno and multiple sensors.

The system is designed to collect liquid level, mass, and temperature measurements, then use these readings to calculate useful parameters such as volume, fill percentage, and density.

A computer running **ROS 2** will receive measurement data over USB serial for further processing and visualization.

> 🚧 **Project status:** Initial planning and design. Hardware integration, firmware development, and ROS 2 functionality will be implemented and validated progressively.

## 🎯 Objectives

- 📏 **Level Measurement** — Measure the distance to the liquid surface using an ultrasonic sensor.
- ⚖️ **Mass Measurement** — Measure mass using a load cell and an appropriate amplifier.
- 🌡️ **Temperature Monitoring** — Monitor liquid temperature within the intended 0–50°C operating range.
- 🧮 **Volume Calculation** — Estimate liquid volume based on tank geometry and level measurements.
- 🧪 **Density Estimation** — Calculate density from corresponding mass and volume measurements.
- 🔌 **Serial Communication** — Transmit sensor readings from Arduino to a computer over USB.
- 🤖 **ROS 2 Integration** — Develop computer-side processing and visualization tools.

## 🏗️ System Architecture

The planned system is divided into three main layers:

```text
┌──────────────────────────────────────┐
│            LIQUID TANK               │
│                                      │
│  Ultrasonic Sensor                   │
│  Load Cell + Amplifier               │
│  Temperature Sensor                  │
└──────────────────┬───────────────────┘
                   │ Sensor Signals
                   ▼
┌──────────────────────────────────────┐
│             ARDUINO UNO              │
│                                      │
│  Sensor Acquisition                  │
│  Data Processing                     │
│  Serial Data Transmission            │
└──────────────────┬───────────────────┘
                   │ USB Serial
                   ▼
┌──────────────────────────────────────┐
│             ROS 2 PC                 │
│                                      │
│  Data Reception                      │
│  Engineering Calculations            │
│  Monitoring & Visualization          │
└──────────────────────────────────────┘
```

_Architecture shown is the proposed design; implementation details may change during development._

## 🔧 Hardware

| Component           | Purpose                                     |
| ------------------- | ------------------------------------------- |
| Arduino Uno         | Main controller for sensor acquisition      |
| Ultrasonic sensor   | Liquid level measurement                    |
| Load cell           | Mass measurement                            |
| Load cell amplifier | Interface between the load cell and Arduino |
| Temperature sensor  | Liquid temperature measurement              |
| Tank structure      | Holds the liquid and supports the sensors   |

Exact component models, electrical connections, and calibration procedures will be documented during hardware development.

## 💻 Software & Technologies

<p>
  <img src="https://img.shields.io/badge/Arduino%20IDE-00979D?style=flat&logo=arduino&logoColor=white" alt="Arduino IDE"/>
  <img src="https://img.shields.io/badge/C%2B%2B-00599C?style=flat&logo=cplusplus&logoColor=white" alt="C++"/>
  <img src="https://img.shields.io/badge/ROS%202-22314E?style=flat&logo=ros&logoColor=white" alt="ROS 2"/>
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black" alt="Linux"/>
  <img src="https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white" alt="Git"/>
  <img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white" alt="GitHub"/>
</p>

- **Embedded development:** Arduino IDE and C++
- **Communication:** USB serial
- **Robotics middleware:** ROS 2
- **Development environment:** Linux
- **Version control:** Git and GitHub

## 📐 Engineering Calculations

The system is intended to derive additional information from sensor measurements.

| Parameter       | Method                                                    |
| --------------- | --------------------------------------------------------- |
| Liquid level    | Tank reference height minus measured surface distance     |
| Fill percentage | Liquid volume divided by tank capacity × 100%             |
| Liquid volume   | Calculated from measured level and tank geometry          |
| Liquid mass     | Load cell reading after calibration and tare compensation |
| Liquid density  | Liquid mass divided by liquid volume                      |

Calculations will account for tank geometry, sensor calibration, measurement uncertainty, and the liquid's physical properties where applicable.

## 📚 Documentation

| Document                                                 | Description                                            |
| -------------------------------------------------------- | ------------------------------------------------------ |
| [Project Proposal](<docs/Team 3_Project proposal.pdf>)   | Project motivation, objectives, scope, and methodology |
| [Literature Review](<docs/Team 3_Literature review.pdf>) | Background research and review of existing approaches  |

Additional design documents, wiring diagrams, and test results will be added as the project progresses.

## 🛠️ Development Roadmap

- [x] Define the initial project scope
- [x] Prepare the project proposal and literature review
- [ ] Finalize hardware components and specifications
- [ ] Design the system architecture and wiring
- [ ] Implement Arduino sensor acquisition
- [ ] Calibrate and validate individual sensors
- [ ] Implement USB serial communication
- [ ] Develop ROS 2 data reception and processing
- [ ] Build monitoring and visualization tools
- [ ] Conduct system-level testing and document results

## 📊 Testing & Validation

Testing will focus on:

- Sensor calibration and repeatability
- Liquid level and volume estimation accuracy
- Load cell accuracy and tare compensation
- Temperature measurement accuracy
- Serial communication reliability
- Comparison of calculated values against reference measurements

Experimental results will be published here once testing begins.

## 🔮 Future Improvements

Potential extensions include:

- Live ROS 2 dashboards and data visualization
- Data logging and historical analysis
- Measurement filtering and noise reduction
- Support for different tank geometries
- Improved calibration and uncertainty analysis

## 👨‍💻 Author

**Mohamed Samer**

Mechatronics Engineering Student

Interested in embedded systems, robotics, automation, and engineering simulation.

---

<p align="center">
  <i>Developed as an educational engineering project exploring embedded systems, instrumentation, and robotics.</i>
</p>
