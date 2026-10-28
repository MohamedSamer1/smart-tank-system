# 🔌 Wiring and Circuit Connections

<p align="center">
  <strong>Smart Tank System</strong><br>
  <em>Hardware Wiring Specification — Arduino Uno R3</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Controller-Arduino%20Uno%20R3-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino Uno R3">
  <img src="https://img.shields.io/badge/Temperature-DS18B20-orange?style=for-the-badge" alt="DS18B20">
  <img src="https://img.shields.io/badge/Ultrasonic-HC--SR04-blue?style=for-the-badge" alt="HC-SR04">
  <img src="https://img.shields.io/badge/Load%20Cell%20ADC-HX711-green?style=for-the-badge" alt="HX711">
</p>

---

## 📌 Overview

This document describes the planned electrical connections for the Smart Tank System using an **Arduino Uno R3**, an **HC-SR04 ultrasonic sensor**, a **DS18B20 temperature sensor**, an **HX711 load-cell amplifier**, and a compatible load cell.

The circuit is designed to acquire liquid level, temperature, and mass measurements. The Arduino will process the readings and transmit data to a computer through USB serial for planned ROS 2 integration.

> ⚠️ **Important:** This document describes the intended connections. Verify the actual pin labels, module specifications, and load-cell wiring before powering the circuit.

## 🧩 1. Components

| Reference | Component                 | Description                            |
| --------- | ------------------------- | -------------------------------------- |
| U1        | Arduino Uno R3            | Main microcontroller                   |
| J2        | DS18B20 connector         | Three-pin temperature sensor interface |
| R1        | 4.7 kΩ resistor           | DS18B20 data-line pull-up              |
| J3        | HX711 interface connector | Four-pin Arduino-to-HX711 connection   |
| J4        | HC-SR04 connector         | Four-pin ultrasonic sensor interface   |
| J5        | Load-cell connector       | Four-wire load-cell interface          |
| C1        | 100 nF capacitor          | Optional local decoupling capacitor    |

The connector references above follow the proposed KiCad schematic. They identify schematic connectors and do not necessarily represent the reference designators printed on physical modules.

## 🧠 2. Arduino Uno R3 Pin Assignment

The following pin assignment will be used for the proposed circuit.

| Arduino Pin | Connected Signal    | Function                     |
| ----------- | ------------------- | ---------------------------- |
| 5V          | Sensor supply rails | Power for compatible modules |
| GND         | Common ground       | Shared electrical reference  |
| D2          | `TEMP_DATA`         | DS18B20 data                 |
| D3          | `HX_DOUT`           | HX711 data output            |
| D4          | `HX_SCK`            | HX711 clock                  |
| D5          | `US_TRIG`           | HC-SR04 trigger              |
| D6          | `US_ECHO`           | HC-SR04 echo                 |

This assignment reserves five digital pins for the three measurement subsystems.

## 🌡️ 3. DS18B20 Temperature Sensor

**Interface:** 1-Wire digital communication  
**Arduino data pin:** D2

The DS18B20 will measure the liquid temperature within the intended project range of 0–50°C.

### Wiring

| DS18B20 Connection | Arduino / Circuit Connection                     |
| ------------------ | ------------------------------------------------ |
| VCC                | +5V, if supported by the selected probe assembly |
| GND                | GND                                              |
| DATA               | Arduino D2 (`TEMP_DATA`)                         |

### Pull-Up Resistor

A **4.7 kΩ resistor (R1)** will connect the data line to the positive supply.

```text
       +5V
        |
      [R1]
      4.7 kΩ
        |
        +---------- TEMP_DATA ---------- Arduino D2
        |
     DS18B20 DATA

     DS18B20 VCC ----------------------- +5V
     DS18B20 GND ----------------------- GND
```

The resistor is a pull-up for the 1-Wire data bus. It does not connect in series with the sensor's power supply.

**Design notes**

- Confirm the probe's actual wire colors and pinout.
- Some probe assemblies include additional wiring or an integrated pull-up; inspect the actual hardware.
- Keep the data connection secure and protected from moisture.

## ⚖️ 4. HX711 Load-Cell Amplifier

**Interface:** Digital data and clock  
**Arduino pins:** D3 and D4

The HX711 converts the small electrical signal produced by a compatible strain-gauge load cell into digital measurements for the Arduino.

### Arduino-to-HX711 Wiring

| HX711 Pin | Arduino Connection                       |
| --------- | ---------------------------------------- |
| VCC       | +5V, if supported by the selected module |
| GND       | GND                                      |
| DT / DOUT | D3 (`HX_DOUT`)                           |
| SCK / CLK | D4 (`HX_SCK`)                            |

```text
Arduino Uno R3             HX711 Module

5V  ---------------------- VCC
GND ---------------------- GND
D3  ---------------------- DT / DOUT
D4  ---------------------- SCK / CLK
```

**Design notes**

- Confirm the power requirements of the actual HX711 breakout board.
- Connect DT and SCK to the corresponding pins, not to the load-cell terminals.
- Keep the load-cell wiring secure and avoid mechanical strain on the connections.
- Calibrate the complete load-cell and amplifier assembly before using its measurements.

## 📏 5. HC-SR04 Ultrasonic Sensor

**Interface:** TRIG and ECHO digital signals  
**Arduino pins:** D5 and D6

The HC-SR04 measures the distance between the sensor and the liquid surface. The Arduino will use this distance to estimate the liquid height.

### Wiring

| HC-SR04 Pin | Arduino Connection |
| ----------- | ------------------ |
| VCC         | +5V                |
| GND         | GND                |
| TRIG        | D5 (`US_TRIG`)     |
| ECHO        | D6 (`US_ECHO`)     |

```text
Arduino Uno R3             HC-SR04

5V  ---------------------- VCC
GND ---------------------- GND
D5  ---------------------- TRIG
D6  ---------------------- ECHO
```

**Design notes**

- Mount the sensor above the liquid surface where practical.
- Keep the sensor electronics away from liquid splashes.
- Verify stable distance readings before integrating volume calculations.
- Avoid obstructing the sensor's acoustic path.

## 🔩 6. Load-Cell Connections

The load cell connects to the **HX711 module**, not directly to the Arduino Uno.

The proposed four-wire load-cell connections are:

| Load-Cell Signal    | HX711 Terminal | Common Wire Color\* |
| ------------------- | -------------- | ------------------- |
| Excitation positive | E+             | Red                 |
| Excitation negative | E−             | Black               |
| Signal positive     | A+             | Green               |
| Signal negative     | A−             | White               |

\*Wire colors are common conventions, not guarantees. The load cell's datasheet or manufacturer wiring diagram takes precedence.

### Signal Path

```text
Load Cell
    |
    | E+, E-, A+, A-
    v
HX711 Amplifier
    |
    | DT / DOUT, SCK
    v
Arduino Uno R3
    |
    | USB Serial
    v
Computer running ROS 2
```

**Important checks**

- Confirm whether the load cell uses four-wire or another wiring arrangement.
- Verify the excitation and signal terminals before connecting it.
- If readings decrease when weight increases, the signal polarity or software calibration may need adjustment.
- Ensure the load cell is mechanically mounted to measure the intended load without unwanted side forces.

## 🗺️ 7. KiCad Connector Assignments

Use the following proposed connector pin assignments in the KiCad schematic.

### J2 — DS18B20 Connector

| Pin | Signal    |
| --- | --------- |
| 1   | +5V       |
| 2   | TEMP_DATA |
| 3   | GND       |

Confirm that this pin order matches the connector footprint and the actual probe wiring.

### J3 — HX711 Arduino Interface

| Pin | Signal    |
| --- | --------- |
| 1   | VCC       |
| 2   | GND       |
| 3   | DT / DOUT |
| 4   | SCK / CLK |

This is the Arduino-facing interface, not the load-cell terminal connector.

### J4 — HC-SR04 Connector

| Pin | Signal |
| --- | ------ |
| 1   | +5V    |
| 2   | TRIG   |
| 3   | ECHO   |
| 4   | GND    |

### J5 — Load-Cell Connector

| Pin | Signal |
| --- | ------ |
| 1   | E+     |
| 2   | E−     |
| 3   | A+     |
| 4   | A−     |

These are proposed schematic pin assignments. Confirm the physical connector pin numbering and orientation before assembling the circuit.

## 🏷️ 8. KiCad Net Labels

Use KiCad's **Place Net Label** tool (`L` shortcut) to name the signals consistently.

| Net Label   | Connection                       |
| ----------- | -------------------------------- |
| `TEMP_DATA` | Arduino D2, DS18B20 DATA, and R1 |
| `HX_DOUT`   | Arduino D3 to HX711 DT/DOUT      |
| `HX_SCK`    | Arduino D4 to HX711 SCK/CLK      |
| `US_TRIG`   | Arduino D5 to HC-SR04 TRIG       |
| `US_ECHO`   | Arduino D6 to HC-SR04 ECHO       |
| `LC_E+`     | Load-cell excitation positive    |
| `LC_E-`     | Load-cell excitation negative    |
| `LC_A+`     | Load-cell signal positive        |
| `LC_A-`     | Load-cell signal negative        |

Use the `+5V` and `GND` power symbols for the appropriate supply rails.

The four `LC_...` labels are optional naming conventions. They must connect to the corresponding load-cell terminals on the HX711 side of the circuit, with no unintended connection to Arduino digital pins.

## ⚡ 9. Power and Ground

For initial prototyping, the Arduino Uno can generally be powered through its USB connection. Its 5V rail may supply compatible sensor modules if the total current demand is within the board's and USB source's limits.

### Power Checklist

- [ ] Connect all required grounds to the common ground.
- [ ] Verify the supply requirements of the Arduino, HX711, and sensors.
- [ ] Check for shorts between +5V and GND before powering the circuit.
- [ ] Confirm the polarity of all connectors.
- [ ] Keep the electronics protected from water and condensation.
- [ ] Verify that the USB connection is stable before starting serial communication.

**C1 — 100 nF decoupling capacitor:** If included, place it close to the supply pins of the relevant module or circuit section. It is optional in the current schematic and does not replace any required module-level decoupling.

## 🧪 10. Initial Testing Procedure

Test each subsystem separately before running the complete system.

1. **Arduino Uno:** Upload a basic sketch and verify that the board communicates over USB.
2. **DS18B20:** Read temperature values and compare them with a reference thermometer.
3. **HC-SR04:** Measure known distances and check the repeatability of readings.
4. **HX711 and load cell:** Read raw values, perform tare compensation, and calibrate using known masses.
5. **Integrated circuit:** Read all sensors together and check for unstable readings or electrical interference.
6. **Serial communication:** Transmit measurement data to the computer and verify that it can be parsed reliably.

Record the pin assignments, calibration constants, test conditions, and observed errors as part of the project documentation.

## 📚 Related Documentation

- [Hardware Components](components.md)
- [Project README](../README.md)
- [Circuit Design PDF](<../docs/Team 3_Circuit design.pdf>)
- [Project Flowchart PDF](<../docs/Team 3_Project flowchart.pdf>)
- [ROS 2 Nodes and Topics PDF](<../docs/Team 3_Nodes&Topics.pdf>)

---

<p align="center">
  <em>Smart Tank System — Wiring documentation for the Arduino Uno R3 prototype.</em>
</p>
