# 🔧 Hardware Components

<p align="center">
  <strong>Smart Tank System</strong><br>
  <em>Hardware Specification and Component Selection</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Controller-Arduino%20Uno-00979D?style=for-the-badge&logo=arduino&logoColor=white" alt="Arduino Uno">
  <img src="https://img.shields.io/badge/Level%20Sensor-HC--SR04-blue?style=for-the-badge" alt="HC-SR04">
  <img src="https://img.shields.io/badge/Temperature-DS18B20-orange?style=for-the-badge" alt="DS18B20">
  <img src="https://img.shields.io/badge/Load%20Cell%20ADC-HX711-green?style=for-the-badge" alt="HX711">
</p>

---

## 📌 Overview

The **Smart Tank System** is an embedded engineering project designed to monitor liquid level, mass, and temperature using an Arduino Uno and dedicated sensors.

The collected measurements will be used to estimate liquid volume, fill percentage, and density. The Arduino will transmit measurement data to a computer over USB serial, with **ROS 2 integration** planned for data processing and visualization.

> 🚧 **Project Status:** Hardware planning and system design. Firmware development, sensor calibration, and integration testing are planned.

## 🧩 Component Summary

| Component           | Model                                    | Purpose                                  |
| ------------------- | ---------------------------------------- | ---------------------------------------- |
| Microcontroller     | Arduino Uno                              | Sensor acquisition and data transmission |
| Ultrasonic Sensor   | HC-SR04                                  | Liquid level measurement                 |
| Temperature Sensor  | DS18B20 waterproof probe                 | Liquid temperature measurement           |
| Load Cell           | To be confirmed                          | Mass measurement                         |
| Load Cell Amplifier | HX711                                    | Load cell signal conversion              |
| Tank                | Dimensions to be confirmed               | Liquid containment and volume reference  |
| USB Cable           | Compatible with the selected Arduino Uno | Programming and serial communication     |
| Connecting Wires    | Suitable for the circuit                 | Electrical connections                   |

## 1. 🧠 Arduino Uno

**Category:** Microcontroller

**Role:** Main embedded controller

The Arduino Uno is responsible for collecting sensor measurements, performing initial data processing, and transmitting measurement data to the computer.

### Planned Responsibilities

- Read distance measurements from the HC-SR04 ultrasonic sensor.
- Acquire load cell readings through the HX711 amplifier.
- Read temperature data from the DS18B20 sensor.
- Format sensor measurements into a consistent data message.
- Transmit measurement data over USB serial for planned ROS 2 integration.

### Design Considerations

- Confirm the available pins before finalizing the circuit.
- Verify the supply voltage and signal-level requirements of each module.
- Use a consistent serial communication format.
- Avoid unnecessary blocking delays that could interfere with sensor readings.

## 2. 📏 Ultrasonic Sensor — HC-SR04

**Category:** Distance measurement  
**Interface:** TRIG and ECHO digital signals

The HC-SR04 measures the distance between the sensor and the liquid surface. This measurement will be used to estimate the liquid height inside the tank.

### Operating Principle

The sensor emits an ultrasonic pulse and measures the time taken for the reflected signal to return.

$$
d = \frac{v_{\text{sound}} \times t}{2}
$$

Where:

- \(d\) is the measured distance.
- \(v\_{\text{sound}}\) is the speed of sound.
- \(t\) is the round-trip travel time of the ultrasonic pulse.
- Division by 2 accounts for the outgoing and returning paths.

For a sensor mounted above the tank, the liquid height can be estimated using:

$$
h = H - d
$$

Where:

- \(h\) is the liquid height.
- \(H\) is the distance from the sensor reference point to the tank bottom.
- \(d\) is the measured distance from the sensor to the liquid surface.

### Integration Considerations

- Connect TRIG and ECHO to suitable Arduino digital pins.
- Power the module according to its specifications.
- Mount the sensor above the liquid surface where practical.
- Keep the sensor electronics protected from moisture and splashes.
- Compare sensor readings with known reference distances.

> ⚠️ The standard HC-SR04 is not waterproof. Condensation, turbulence, and irregular liquid surfaces may also affect measurement reliability.

## 3. 🌡️ Temperature Sensor — DS18B20 Waterproof Probe

**Category:** Temperature measurement  
**Interface:** 1-Wire digital communication  
**Intended project range:** 0–50°C

The waterproof DS18B20 probe will measure the liquid temperature and provide digital readings to the Arduino.

### Planned Responsibilities

- Measure the temperature of the test liquid.
- Supply temperature readings for monitoring and data logging.
- Provide additional information for interpreting liquid measurements.

### Integration Considerations

- Connect the data line to a suitable Arduino digital pin.
- Use the required data-line pull-up resistor, commonly 4.7 kΩ, unless the selected module already includes one.
- Verify the probe wiring and pinout before connecting power.
- Confirm that the probe materials are compatible with the intended liquid.
- Validate readings against a suitable reference thermometer.

The DS18B20 sensing element supports a wider temperature range than the project's intended 0–50°C range. The complete probe assembly must also be suitable for the intended application.

## 4. ⚖️ Load Cell

**Category:** Force and mass measurement  
**Model:** To be confirmed  
**Rated capacity:** To be determined

The load cell will measure the load supported by the tank platform. After calibration and tare compensation, the system will estimate the mass of the liquid.

### Selection Requirements

- Sufficient rated capacity for the tank, maximum liquid mass, and supported hardware.
- Compatibility with the HX711 amplifier.
- Suitable mechanical mounting and load direction.
- Adequate resolution and repeatability for the intended measurements.

### Calibration Procedure

1. Record the unloaded or empty-tank reading.
2. Apply known reference masses.
3. Determine the calibration factor.
4. Verify the calibration using additional reference masses.
5. Apply tare compensation during normal operation.

The load cell model, rated capacity, wiring, and calibration factor will be documented once finalized.

## 5. 🔌 Load Cell Amplifier — HX711

**Category:** Signal conditioning and analog-to-digital conversion  
**Interface:** DT (data) and SCK (clock)

The HX711 amplifies the small differential signal produced by a compatible strain-gauge load cell and converts it into digital measurements that the Arduino can read.

### Planned Responsibilities

- Read the electrical output from the load cell.
- Convert the signal into digital measurements.
- Provide measurement data to the Arduino for processing.
- Support load cell calibration and tare compensation.

### Integration Considerations

- Connect the load cell according to the wiring documentation for the selected components.
- Connect DT and SCK to suitable Arduino digital pins.
- Confirm the amplifier board's supply and logic-voltage requirements.
- Ensure the load cell is mechanically mounted correctly.
- Calibrate the complete load cell and amplifier assembly.

The HX711 does not eliminate the need for proper mechanical installation or calibration.

## 6. 🛢️ Liquid Tank and Mechanical Structure

**Category:** Mechanical assembly

**Role:** Liquid containment and measurement reference

The tank will contain the test liquid and provide the geometry required to convert measured liquid height into volume.

### Design Requirements

- Known internal dimensions and capacity.
- Secure mounting for the HC-SR04.
- Stable load transfer to the load cell.
- Suitable material for the intended liquid.
- Appropriate placement for the DS18B20 probe.
- Protection of electrical components from leaks and spills.

### Specifications to Confirm

- Tank shape: To be determined.
- Internal dimensions: To be measured.
- Maximum capacity: To be determined.
- Material: To be selected.
- Sensor mounting positions: To be finalized.

## 7. 🔗 USB Connection and Wiring

**Category:** Electrical interconnection and communication

The Arduino Uno will connect to the computer through USB for programming and serial data transmission.

Connecting wires will link the ultrasonic sensor, temperature sensor, and HX711 amplifier to the Arduino according to the finalized circuit diagram.

### Design Considerations

- Verify supply voltage and pin assignments before powering the circuit.
- Maintain appropriate common-ground connections where required.
- Secure and insulate exposed wiring.
- Protect electronic modules from liquid exposure.
- Confirm the serial settings and detected USB serial device during integration.

## 📐 Engineering Calculations

The system will use sensor measurements to estimate useful liquid parameters.

### 1. Liquid Height

For a sensor mounted above the tank:

$$
h = H - d
$$

Where \(H\) is the reference height and \(d\) is the measured distance to the liquid surface.

### 2. Liquid Volume

For a tank with a constant horizontal cross-sectional area:

$$
V = A \times h
$$

Where:

- \(V\) is the liquid volume.
- \(A\) is the internal cross-sectional area.
- \(h\) is the liquid height.

For tanks with changing cross-sectional area, the volume calculation must account for the actual tank geometry.

### 3. Fill Percentage

$$
\text{Fill Percentage} =
\frac{V_{\text{liquid}}}{V_{\text{tank}}}
\times 100\%
$$

Where:

- \(V\_{\text{liquid}}\) is the estimated liquid volume.
- \(V\_{\text{tank}}\) is the usable tank capacity.

### 4. Liquid Mass

The liquid mass will be estimated from the calibrated load cell measurement after accounting for the empty tank and other supported hardware.

$$
m_{\text{liquid}} =
m_{\text{measured}} - m_{\text{empty tank}}
$$

This simplified equation assumes that the empty-tank measurement includes all other supported hardware and that the mechanical setup remains unchanged.

### 5. Liquid Density

$$
\rho = \frac{m_{\text{liquid}}}{V_{\text{liquid}}}
$$

Where:

- \(\rho\) is the estimated liquid density.
- \(m\_{\text{liquid}}\) is the liquid mass.
- \(V\_{\text{liquid}}\) is the liquid volume.

Density should only be calculated when the mass and volume measurements are valid and the volume is sufficiently greater than zero.

## 🔬 Calibration and Validation

Each measurement subsystem will be tested before full system integration.

- **HC-SR04:** Compare measured distances against known reference distances.
- **DS18B20:** Compare temperature readings against a reference thermometer.
- **Load Cell + HX711:** Calibrate using known masses and verify tare compensation.
- **Volume Calculation:** Compare estimated volume against a known quantity of liquid.
- **Serial Communication:** Check message formatting, data consistency, and communication reliability.
- **System Integration:** Compare the combined system's calculated values against reference measurements.

Calibration values, test procedures, and experimental errors will be recorded as development progresses.

## 📚 Related Documentation

- 📄 [Project Proposal](<../docs/Team 3_Project proposal.pdf>) — Project objectives, scope, and methodology.
- 📖 [Literature Review](<../docs/Team 3_Literature review.pdf>) — Background research and existing approaches.
- 🔌 [Circuit Design](<../docs/Team 3_Circuit design.pdf>) — Planned electrical connections between the Arduino Uno and sensors.
- 🤖 [ROS 2 Nodes and Topics](<../docs/Team 3_Nodes&Topics.pdf>) — Proposed nodes, topics, and communication architecture.
- 🔄 [Project Flowchart](<../docs/Team 3_Project flowchart.pdf>) — Planned system logic and operational workflow.

---

<p align="center">
  <em>Smart Tank System — Hardware documentation maintained throughout development.</em>
</p>
