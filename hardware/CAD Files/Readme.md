# 🧩 Mechanical Design — SolidWorks

## 1. Overview

The mechanical design of the Smart Tank System was developed using **SolidWorks**.

The design includes a cylindrical liquid tank, supporting brackets, sensor mounting arrangements, and a complete mechanical assembly.

The CAD model provides a three-dimensional representation of the mechanical structure and the arrangement of its components.

## 2. Mechanical Components

The SolidWorks model consists of:

- **Cylindrical Tank:** Contains the liquid being monitored.
- **Load-Cell Brackets:** Support the tank and accommodate the load-cell mounting arrangement.
- **Top Cover:** Covers the tank and provides the mounting arrangement for the ultrasonic sensor.
- **Ultrasonic Sensor Mounting:** Positions the HC-SR04 above the tank, facing the liquid surface.
- **Temperature Probe Opening:** An opening near the bottom of the tank for inserting the waterproof DS18B20 temperature probe.

## 3. Mechanical Assembly

The individual SolidWorks parts have been combined into a complete mechanical assembly.

The assembly represents the overall arrangement of the tank, cover, sensor mounting positions, and supporting structure.

## 4. Assembly Visualization

### 4.1 Isometric View

<p align="center">
  <img src="Renders/Isometric%20Assem.png" alt="Smart Tank System Isometric Assembly" width="85%">
</p>

### 4.2 Front View

<p align="center">
  <img src="Renders/Front%20Assem.png" alt="Smart Tank System Front Assembly" width="85%">
</p>

### 4.3 Front Section View

<p align="center">
  <img src="Renders/Section%20Front%20Assem.png" alt="Smart Tank System Front Section Assembly" width="85%">
</p>

### 4.4 Isometric Section View

<p align="center">
  <img src="Renders/Section%20Isometric%20Assem.png" alt="Smart Tank System Isometric Section Assembly" width="85%">
</p>

## 5. Design Considerations

- The HC-SR04 ultrasonic sensor must face the liquid surface.
- The DS18B20 temperature probe must be positioned to measure the liquid temperature.
- The temperature probe opening must be sealed appropriately to prevent liquid leakage.
- The load-cell mounting arrangement must direct the intended tank load through the sensing element.
- The tank must provide sufficient internal space for the intended liquid capacity.
- Sensor mounting positions must allow proper installation and maintenance.

## 6. CAD Directory Structure

```text
CAD Files/
├── Renders/
│   ├── Front Assem.png
│   ├── Isometric Assem.png
│   ├── Section Front Assem.png
│   └── Section Isometric Assem.png
│
└── Readme.md
```

The native SolidWorks parts and assembly files are maintained in their respective project directories.

## 7. Design Status

**Mechanical modeling completed.**

- [x] Create individual mechanical components.
- [x] Model the cylindrical tank.
- [x] Design the load-cell brackets.
- [x] Model the top cover and ultrasonic sensor mounting.
- [x] Add the temperature probe opening.
- [x] Assemble the mechanical components in SolidWorks.
- [x] Prepare front and isometric assembly views.
- [x] Prepare front and isometric section views.

The initial mechanical modeling and assembly objectives have been completed. The SolidWorks assembly will serve as the mechanical reference for the upcoming hardware integration stage.

---

<p align="center">
  <i>Smart Tank System — Mechanical Design</i>
</p>
