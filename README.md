# HLR Car Driving Simulator 

## Project Overview

This project involves converting a broken Volkswagen Golf 4 instrument cluster into a fully functional virtual dashboard for vehicle simulation.  
All parts are sourced from a Golf 4, including the instrument cluster shell, turn signal stalk, and wiper stalk.  
The original gauge stepper motors and electronics were removed and replaced with standard hobby servos and custom 3D-printed gearboxes.  
An Arduino is used to process both control inputs from the stalks and telemetry data from SimHub, allowing the cluster to behave as if it were still installed in the vehicle.

The goal of this project is to create a realistic and durable dashboard using readily available components, while maintaining the authentic look and feel of the original Golf 4 interior.

---

## Components

- Arduino Pro Micro (or Nano ESP32)
- Golf 4 instrument cluster shell
- Golf 4 turn signal stalk
- Golf 4 wiper stalk
- 4× standard hobby servos (speedometer, tachometer, fuel, temperature)
- Custom 3D-printed gearboxes for servo-to-gauge drive
- Resistors for analog ladder circuits
- USB cable and basic wiring

---

## Features

- Uses original Golf 4 stalks for control input
- Reads multiple button/switch states using analog resistor ladders
- Emulates joystick buttons through Arduino HID
- Drives analog speedometer, tachometer, fuel, and temperature gauges using servos
- Receives telemetry from SimHub over serial
- Designed to be plug-and-play over USB

---

## SimHub Serial Data Format

The Arduino expects data from SimHub in the following order, each value on a separate line:


---

## Pin Mapping

| Arduino Pin | Function                          | Type                       |
|-------------|------------------------------------|----------------------------|
| A0          | Turn stalk +/- buttons             | Analog (resistor ladder)   |
| A1          | Turn stalk 3-position switch       | Analog (resistor ladder)   |
| A2          | Wiper stalk OK / UP / DOWN buttons | Analog (resistor ladder)   |
| A3          | Wiper stalk 4-step rotary switch   | Analog (resistor ladder)   |
| D2–D5       | Servo outputs (speed, RPM, fuel, temp) | PWM                     |
| USB         | HID joystick and SimHub serial     | Data connection            |

---

## Assembly

1. **Instrument Cluster**  
   Disassemble the original Golf 4 cluster. Remove all electronics and stepper motors.  
   Install the servos and 3D-printed gearboxes behind the gauge faces, aligning them with the original needle axes.

2. **Stalk Inputs**  
   Connect the turn signal and wiper stalks to the Arduino.  
   Use resistor ladder circuits to read multiple positions on a single analog pin.

3. **Wiring and Programming**  
   Connect servos to the appropriate digital pins and flash the provided Arduino sketch.  
   The Arduino will appear as both a joystick (for input) and a serial device (for telemetry).

4. **SimHub Configuration**  
   Set up a custom serial output profile in SimHub to match the expected data format.  
   Once connected, the gauges and inputs will function in real time.

---

## 3D Printed Components

- Gearbox assemblies for servo-to-needle drive
- Mounting brackets and supports for servos inside the cluster shell

STL files are included in the `3d/` folder.

---

## License

This project is released under the MIT License. It may be modified and adapted for educational or personal use.

---

## Acknowledgements

This documentation was prepared for RoboChallenge. All hardware components are original Volkswagen Golf 4 parts.
