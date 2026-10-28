# Smart Tank System — Engineering Calculations

## 1. Overview

This document describes the engineering equations that will be used to calculate liquid level, volume, fill percentage, liquid mass, and density in the Smart Tank System.

The system will use an Arduino Uno R3 with an HC-SR04 ultrasonic sensor, a DS18B20 temperature sensor, and a load cell connected through an HX711 amplifier.

The calculated measurements will later be transmitted to ROS 2 for processing and visualization.

**Note:** The equations and example values in this document are for design and development. Final calculations will use the actual tank dimensions and calibrated sensor readings.

---

## 2. Ultrasonic Distance Measurement

The HC-SR04 will measure the distance between the sensor and the liquid surface.

The sensor measures the time taken by an ultrasonic pulse to travel to the liquid surface and return.

### Equation

$$
d = \frac{v_{\text{sound}} \times t}{2}
$$

Where:

- \(d\) = distance between the sensor and liquid surface (m)
- \(v\_{\text{sound}}\) = speed of sound in air (m/s)
- \(t\) = measured round-trip time (s)
- The factor \(2\) accounts for the outgoing and returning sound waves.

At approximately 20°C, the speed of sound in air is approximately 343 m/s. It varies with air temperature.

If the sensor library returns distance directly, the Arduino will use that reading instead of calculating distance from the pulse time manually.

### Liquid Level

If the ultrasonic sensor is mounted above the tank and the reference distance from the sensor to the tank bottom is known, the liquid height can be calculated as:

$$
h = H-d
$$

Where:

- \(h\) = liquid height (m)
- \(H\) = reference distance from the sensor to the tank bottom (m)
- \(d\) = measured distance from the sensor to the liquid surface (m)

The calculated height must be limited to the tank's valid range:

$$
0 \leq h \leq H_{\text{liquid}}
$$

Here, \(H\_{\text{liquid}}\) is the maximum usable liquid height. The sensor's mounting position and any unusable space near the top or bottom must be considered.

---

## 3. Tank Volume

The tank is planned to use a cylindrical geometry.

### Cylindrical Tank Volume

The liquid volume will be calculated from the internal radius of the tank and the measured liquid height.

$$
V = \pi r^2h
$$

Where:

- \(V\) = liquid volume (m³)
- \(r\) = internal tank radius (m)
- \(h\) = liquid height (m)
- \(\pi\) ≈ 3.14159

The internal dimensions must be used because the liquid occupies the inside of the tank, not the tank walls.

### Conversion to Litres

Since one cubic metre equals 1,000 litres:

$$
V_L = 1000V
$$

Where \(V_L\) is the liquid volume in litres.

### Example

For an illustrative tank with an internal radius of 0.10 m and a liquid height of 0.30 m:

$$
V = \pi (0.10)^2(0.30)
$$

$$
V \approx 0.009425 \text{ m}^3
$$

$$
V_L \approx 9.425 \text{ L}
$$

These are example dimensions, not the final dimensions of the project tank.

---

## 4. Fill Percentage

The fill percentage indicates how much of the tank's usable capacity is occupied by liquid.

$$
\text{Fill Percentage} =
\frac{V_{\text{current}}}{V_{\text{capacity}}}
\times 100
$$

Where:

- \(V\_{\text{current}}\) = current liquid volume
- \(V\_{\text{capacity}}\) = usable tank capacity

For a vertical cylindrical tank with a constant cross-sectional area, the fill percentage can also be calculated from height:

$$
\text{Fill Percentage} =
\frac{h}{H_{\text{liquid}}}\times 100
$$

This height-based equation is valid when the tank has a constant cross-section and the usable liquid height is correctly defined.

The result will be constrained to the range 0–100% for valid measurements. Out-of-range raw readings should also be flagged as possible sensor or calibration errors rather than silently treated as valid.

---

## 5. Load Cell and Liquid Mass

The load cell will measure the weight force applied to it. The HX711 will amplify and digitize the load-cell signal.

The system will calibrate the raw HX711 reading using a known reference mass.

### Calibrated Mass

After calibration, the system will obtain the measured mass in kilograms:

$$
m_{\text{liquid}} =
m_{\text{measured}} - m_{\text{empty tank}}
$$

Where:

- \(m\_{\text{liquid}}\) = estimated liquid mass (kg)
- \(m\_{\text{measured}}\) = total measured mass of the tank and its contents (kg)
- \(m\_{\text{empty tank}}\) = measured mass of the empty tank and any components supported by the load cell (kg)

The empty-tank tare value must be measured with the tank and mounted components in their normal configuration.

### Calibration Procedure

1. Read the HX711 with no load applied, as appropriate for the calibration procedure.
2. Place a known reference mass on the load cell or assembled tank platform.
3. Calculate or adjust the calibration factor.
4. Repeat with additional known masses to check consistency.
5. Record the tare value and calibration factor.
6. Verify the readings after the complete mechanical assembly is installed.

The load-cell mounting must ensure that the intended load passes through the sensing element without being bypassed by other supports.

---

## 6. Liquid Density

Density is the mass of a substance per unit volume.

$$
\rho = \frac{m_{\text{liquid}}}{V}
$$

Where:

- \(\rho\) = liquid density (kg/m³)
- \(m\_{\text{liquid}}\) = liquid mass (kg)
- \(V\) = liquid volume (m³)

If volume is available in litres, it must be converted to cubic metres first:

$$
V = \frac{V_L}{1000}
$$

Therefore:

$$
\rho = \frac{1000m_{\text{liquid}}}{V_L}
$$

Density will only be calculated when both mass and volume are valid and the volume is greater than zero.

The density calculation is sensitive to errors in both the load-cell reading and the ultrasonic measurement. Calibration and comparison against known water quantities will help evaluate its accuracy.

---

## 7. Temperature Measurement

The DS18B20 will measure the liquid temperature.

The sensor provides a temperature reading in degrees Celsius, which will be used for monitoring and displayed by the ROS 2 interface.

The planned operating range for this project is 0–50°C.

The temperature reading may also be used to estimate the speed of sound in air for the ultrasonic calculation. However, the DS18B20 measures liquid temperature, not necessarily the air temperature above the liquid. Using liquid temperature as air temperature may introduce distance error, so the initial implementation may use a nominal speed of sound and evaluate the error experimentally.

The temperature reading will be checked for sensor errors and values outside the intended project range.

---

## 8. Measurement Validation

Before calculating volume, fill percentage, or density, the system will validate its sensor readings.

Planned checks include:

- Rejecting invalid ultrasonic readings or readings outside the sensor's usable range.
- Checking that the calculated liquid height is within the tank's usable height.
- Checking for disconnected or invalid temperature-sensor readings.
- Rejecting invalid HX711 readings and negative liquid mass beyond the expected measurement tolerance.
- Avoiding density calculations when volume is zero or invalid.
- Flagging sensor errors and implausible measurement changes.
- Ensuring that displayed values include the correct units.

A valid zero-level reading must be distinguished from a sensor failure.

---

## 9. ROS 2 Data Flow

The Arduino will acquire the raw sensor readings and send them to the computer over USB serial.

The planned ROS 2 processing node will use these readings to calculate:

- Liquid level (m)
- Liquid volume (L)
- Fill percentage (%)
- Liquid mass (kg)
- Liquid density (kg/m³)
- System status

The GUI node will display sensor readings, calculated values, and any detected errors.

Final topic names, message types, and units will be documented in the ROS 2 nodes-and-topics document.

---

## 10. Testing and Verification

The calculations will be verified experimentally after the tank and sensors are assembled.

Planned tests include:

1. Measure the empty tank and record the reference values.
2. Add known quantities of water in measured increments.
3. Compare the calculated liquid height with a physical measurement.
4. Compare the calculated volume with the quantity added.
5. Compare load-cell measurements against known masses.
6. Compare the temperature sensor with a reference thermometer.
7. Calculate the measurement error for each test.

### Percentage Error

When a reference value is available:

$$
\text{Percentage Error} =
\frac{|\text{Measured Value}-\text{Reference Value}|}
{|\text{Reference Value}|}
\times 100
$$

Percentage error should not be used when the reference value is zero. In that case, report the absolute error instead.

The measured results, calibration factors, and final accuracy will be added after testing. No accuracy value will be claimed until it has been experimentally verified.

---

## 11. Future Improvements

Possible future improvements include:

- Filtering noisy sensor readings.
- Evaluating ultrasonic compensation using air temperature.
- Improving calibration and repeatability.
- Adding configurable low-level and high-level alerts.
- Logging measurements for analysis.
- Comparing measured water density with a reference value at the measured temperature.
