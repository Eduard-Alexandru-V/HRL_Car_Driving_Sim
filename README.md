# HLR Car Driving Simulator 


## Table of Contents
- [Project Overview](#project-overview)
- [Components Overview](#components-overview)
- [Features](#features)
- [SimHub Integration](#simhub-serial-data-format)
- [Pin Mapping](#pin-mapping)
- [Assembly Guide](#assembly)
- [3D Printed Components](#3d-printed-components)
- [License](#license)
- [Acknowledgements](#acknowledgements)

  

## Project Overview

This project involves converting a broken Volkswagen Golf 4 instrument cluster into a fully functional virtual dashboard for vehicle simulation.  
All parts are sourced from a Golf 4, including the instrument cluster shell, turn signal stalk, and wiper stalk.  
The original gauge stepper motors and electronics were removed and replaced with standard hobby servos and custom 3D-printed gearboxes.  
An Arduino is used to process both control inputs from the stalks and telemetry data from SimHub, allowing the cluster to behave as if it were still installed in the vehicle.

The goal of this project is to create a realistic and durable dashboard using readily available components, while maintaining the authentic look and feel of the original Golf 4 interior.



---

## Components Overview

| Component | Description | Photo |
|-----------|-------------|-------|
| Arduino Pro Micro  | Microcontroller that reads the stalk inputs, controls the servos, and communicates with SimHub over USB. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/arduino%20pro%20micro.jpeg?raw=true" alt="Arduino Pro Micro" width="200"> |
| 4 Relay Module | Controls the turn signal lights, sound , high beams and the backlighting from the cluster | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/4%20Relay%20Module.jpeg?raw=true" width="200"> |
| 2 Position Switch | Sends a signal to the arduino to turn on the backlight and the main beams in the game | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/2%20Position%20Switch.jpeg?raw=true" alt="Cluster" width="200"> |
| Golf 4 Instrument Cluster Shell | Original dashboard housing; holds the servos and gearboxes, preserving the original look. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/cluster.jpeg?raw=true" alt="Cluster" width="200"> |
| Golf 4 Turn Signal Stalk | Provides left/right indicators and +/- buttons; input read via resistor ladder. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/turn%20stalk.jpeg?raw=true" alt="Turn Singnal Stalk" width="200"> |
| Golf 4 Wiper Stalk | Provides OK / UP / DOWN buttons and 4-step rotary switch; input read via resistor ladder. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/wiper%20stalk.jpeg?raw=true" alt="Wiper Stalk" width="200"> |
| Standard Hobby Servos (x4) | Drives the speedometer, tachometer, fuel, and temperature gauges via 3D-printed gearboxes (only for the tachometer and speedometer). | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/servo.jpeg?raw=true" alt="SG90 Servo" width="200"> |
| Custom 3D-Printed Gearboxes | Converts servo rotation to the original gauge needle movement; fits inside the cluster shell. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/Gearbox.jpeg?raw=true" alt="Gearbox" width="200"> |
| Resistors for Ladder Circuits | Used to differentiate multiple switch positions on single analog lines. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/resistors.jpeg?raw=true" alt="Resistors" width="200"> |
| USB Cable | Provides power and allows the Arduino to act as a joystick + serial device for SimHub. | <img src="https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/blob/main/images/USB%20C%20cable.jpeg?raw=true" alt="USB C Cable" width="200"> |


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

| Arduino Pin | Function                           | Type                        |
|-------------|------------------------------------|----------------------------|
| A0          | Turn stalk +/- buttons             | Analog (resistor ladder)   |
| A1          | Turn stalk 3-position switch       | Analog (resistor ladder)   |
| A2          | Wiper stalk OK / UP / DOWN buttons | Analog (resistor ladder)   |
| A3          | Wiper stalk 4-step rotary switch   | Analog (resistor ladder)   |
| D2–D5       | Servo outputs (speed, RPM, fuel, temp) | PWM                    |
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

STL files are included in the [`/STL`](https://github.com/Eduard-Alexandru-V/HRL_Car_Driving_Sim/tree/main/STL)  folder.

---

## License

This project is released under the MIT License. It may be modified and adapted for educational or personal use.

---

## Acknowledgements

This documentation was prepared for RoboChallenge. All hardware components are original Volkswagen Golf 4 parts.
