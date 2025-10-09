# HLR Car Driving Simulator 


## Table of Contents
- [Project Overview](#project-overview)
- [Components Overview](#components-overview)
- [Features](#features)
- [SimHub Integration](#simhub-serial-data-format)
- [Pin Mapping](#pin-mapping)
- [Assembly Guide](#assembly)
- [3D Printed Components](#3d-printed-components)
- [Arduino Part](#arduino-part)
  - [Serial Telemetry Input](#serial-telemetry-input)
  - [Servos](#servos)
  - [Relays](#relays)
  - [Stalk Inputs](#stalk-inputs)
  - [Keyboard Emulation](#keyboard-emulation)
  - [Serial Console Commands](#serial-console-commands)
  - [Arduino Code](#arduino-code)
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

## Arduino Part

This Arduino Pro Micro sketch serves as the unified firmware for the Golf 4 virtual dashboard project. It interfaces with SimHub via a 7-line serial telemetry stream and controls servo-driven analog gauges, stalk inputs, and relay outputs to replicate the original dashboard behavior.

### Serial Telemetry Input (from SimHub) <a id="serial-telemetry-input"></a>
The firmware expects **7 lines of data** in this order:

1. Engine RPM  
2. Vehicle Speed (km/h)  
3. Oil Temperature (°C)  
4. Fuel Level (%)  
5. Instant Consumption (L/100 km)  
6. Left Turn Indicator (0 or 1)  
7. Right Turn Indicator (0 or 1)

These values are received sequentially, then mapped to servo angles and relay states to update the gauges and lighting indicators in real time.

### Servos
Four servo motors are used to drive the original Golf 4 gauge needles through custom 3D-printed gearboxes:

- RPM Gauge (1:1.5 gearbox)  
- Speed Gauge (1:1.5 gearbox)  
- Fuel Gauge (direct drive)  
- Temperature Gauge (direct drive)

Calibration for input and servo ranges can be adjusted through the serial console using commands such as `set rpmmin`, `set speedservomax`, etc. Servo angles are computed using a linear mapping function with optional gearbox scaling.

### Relays
Four digital outputs control relays that drive external lighting or indicator circuits:

- Left Turn Signal  
- Right Turn Signal  
- High Beam  
- Custom Switch (manual input)

The high beam state can be read either from a digital input or one of the analog ladder inputs, allowing flexible integration with the existing stalk hardware.

### Stalk Inputs
All stalk buttons and switches from the Golf 4 assembly are connected to the Pro Micro’s analog pins through resistor ladders:

- **A0:** Turn stalk +/- buttons  
- **A1:** 3-position switch (ON / CANCEL / OFF)  
- **A2:** Wiper OK / TOP / DOWN buttons  
- **A3:** Wiper 4-step rotary switch  

Analog thresholds are defined in the code for each input state. These inputs can also trigger keyboard HID outputs to interact with software or games.

### Keyboard Emulation
The firmware uses the Arduino Keyboard library to send key presses based on stalk input events and turn signal changes. This allows the dashboard and stalks to be recognized as a virtual game controller or keyboard by the host PC without additional drivers.

### Serial Console Commands
The firmware includes a basic line-based command system for runtime calibration and testing:

- `set <key> <value>` – adjust input or servo calibration values  
- `test <rpm|speed|fuel|temp> <value>` – manually move servo to a position  
- `show` – display current calibration settings

These commands do not persist after reset and are intended for quick tuning during installation.

## Arduino Code

```cpp
#include <Servo.h>
#include <Keyboard.h>

// --- Pin configuration ---
const uint8_t PIN_A0 = A0; // Turn stalk +/- ladder input
const uint8_t PIN_A1 = A1; // Turn stalk 3-position switch input
const uint8_t PIN_A2 = A2; // Wiper stalk OK/TOP/DOWN ladder input
const uint8_t PIN_A3 = A3; // Wiper 4-step ladder input

const bool HIGHBEAM_IS_ANALOG = true; // High beam read mode
const uint8_t HIGHBEAM_ANALOG_INDEX = 0; // Which analog pin for high beam
const uint16_t HIGHBEAM_ANALOG_THRESHOLD = 500; // Threshold for analog high beam

const uint8_t PIN_HIGHBEAM_DIGITAL = 2; // High beam digital input if analog not used
const uint8_t PIN_FLASH_DIGITAL = 3;   // Optional flash input

// Servo pins
const uint8_t PIN_SERVO_RPM   = 5;
const uint8_t PIN_SERVO_SPEED = 6;
const uint8_t PIN_SERVO_TEMP  = 9;
const uint8_t PIN_SERVO_FUEL  = 10;

// Relay pins
const uint8_t PIN_RELAY_RIGHT  = 14;
const uint8_t PIN_RELAY_LEFT   = 15;
const uint8_t PIN_RELAY_HIGH   = 16;
const uint8_t PIN_RELAY_CUSTOM = 7;

// Manual switch input for relay 4
const uint8_t PIN_MANUAL_SWITCH_IN = 11;

// Buzzer pin
const uint8_t PIN_BUZZER = 4;

// --- Max telemetry values ---
const int MAX_RPM   = 7500;
const int MAX_SPEED = 260;
const int MAX_FUEL  = 100;
const int MAX_TEMP  = 120;

// Gearbox ratio for RPM/Speed servos
const float GEARBOX_RATIO = 1.5f;

// Servo calibration (adjustable via serial)
int rpmInputMin = 0, rpmInputMax = MAX_RPM;
int rpmServoMin = 0, rpmServoMax = 120;
int speedInputMin = 0, speedInputMax = MAX_SPEED;
int speedServoMin = 0, speedServoMax = 120;
int fuelServoMin = 0, fuelServoMax = 90;
int tempServoMin = 0, tempServoMax = 90;

// --- Globals ---
Servo servoRPM, servoSpeed, servoFuel, servoTemp;
String simLines[7]; // Store telemetry lines
uint8_t simIndex = 0;
unsigned long lastSimReceive = 0;
const unsigned long SIM_TIMEOUT_MS = 250; // Reset if partial data

// Stalk button thresholds
const int A0_MINUS_TH = 400;
const int A0_PLUS_TH  = 500;
const int A2_OK_TH  = 70;
const int A2_TOP_TH = 110;
const int A2_DOWN_TH = 250;
const int A3_STEP1_TH = 30;
const int A3_STEP2_TH = 100;
const int A3_STEP3_TH = 150;
const int A3_STEP4_TH = 300;

// Keyboard mappings
const uint8_t KEY_TURN_LEFT_PRESS  = 'q';
const uint8_t KEY_TURN_RIGHT_PRESS = 'e';
const uint8_t KEY_HIGHBEAM_PRESS   = 'h';
const uint8_t KEY_FLASH_PRESS      = 'f';

// --- Setup ---
void setup() {
  Serial.begin(115200);
  while (!Serial) {} // Wait for host

  // Attach servos
  servoRPM.attach(PIN_SERVO_RPM);
  servoSpeed.attach(PIN_SERVO_SPEED);
  servoFuel.attach(PIN_SERVO_FUEL);
  servoTemp.attach(PIN_SERVO_TEMP);

  // Configure relay pins
  pinMode(PIN_RELAY_RIGHT, OUTPUT);
  pinMode(PIN_RELAY_LEFT, OUTPUT);
  pinMode(PIN_RELAY_HIGH, OUTPUT);
  pinMode(PIN_RELAY_CUSTOM, OUTPUT);

  pinMode(PIN_MANUAL_SWITCH_IN, INPUT_PULLUP);
  if (!HIGHBEAM_IS_ANALOG) pinMode(PIN_HIGHBEAM_DIGITAL, INPUT_PULLUP);
  pinMode(PIN_FLASH_DIGITAL, INPUT_PULLUP);

  pinMode(PIN_BUZZER, OUTPUT);
  digitalWrite(PIN_RELAY_RIGHT, LOW);
  digitalWrite(PIN_RELAY_LEFT, LOW);
  digitalWrite(PIN_RELAY_HIGH, LOW);
  digitalWrite(PIN_RELAY_CUSTOM, LOW);

  Keyboard.begin();

  Serial.println(F("Unified Dash Firmware started."));
  Serial.println(F("Waiting for SimHub 7-line data..."));
  Serial.println(F("Serial commands: set <key> <val>, test <servo> <val>, show"));
}

// --- Helper functions ---
int safeMapConstrain(int in, int inMin, int inMax, int outMin, int outMax) {
  if (inMax == inMin) return outMin;
  long val = map(constrain(in, inMin, inMax), inMin, inMax, outMin, outMax);
  return constrain(val, min(outMin,outMax), max(outMin,outMax));
}

// Read high beam state
int readHighBeamState() {
  if (HIGHBEAM_IS_ANALOG) {
    int adc = analogRead(PIN_A0 + HIGHBEAM_ANALOG_INDEX);
    return (adc >= HIGHBEAM_ANALOG_THRESHOLD) ? 1 : 0;
  } else {
    return digitalRead(PIN_HIGHBEAM_DIGITAL) == LOW ? 1 : 0;
  }
}

// Read A0 ladder buttons
bool readA0_minus() { return analogRead(PIN_A0) < A0_MINUS_TH; }
bool readA0_plus()  { int v = analogRead(PIN_A0); return (v < A0_PLUS_TH && v >= A0_MINUS_TH); }

// Wiper buttons
int readWiperButtonsA2() {
  int v = analogRead(PIN_A2);
  if (v < A2_OK_TH) return 1;
  if (v < A2_TOP_TH) return 2;
  if (v < A2_DOWN_TH) return 3;
  return 0;
}

// Wiper step switch
int readWiperStepA3() {
  int v = analogRead(PIN_A3);
  if (v < A3_STEP1_TH) return 1;
  if (v < A3_STEP2_TH) return 2;
  if (v < A3_STEP3_TH) return 3;
  if (v < A3_STEP4_TH) return 4;
  return 0;
}

// --- Serial console parser ---
void handleSerialConsole(String cmd) {
  cmd.trim();
  if (cmd.length() == 0) return;

  int firstSpace = cmd.indexOf(' ');
  String word1 = (firstSpace == -1) ? cmd : cmd.substring(0, firstSpace);
  word1.toLowerCase();

  if (word1 == "set") {
    String rest = cmd.substring(firstSpace + 1);
    int sp = rest.indexOf(' ');
    if (sp == -1) { Serial.println(F("Usage: set <key> <value>")); return; }
    String key = rest.substring(0, sp);
    int val = rest.substring(sp + 1).toInt();

    if (key == "rpmmin") rpmInputMin = val;
    else if (key == "rpmmax") rpmInputMax = val;
    else if (key == "rpmservomin") rpmServoMin = val;
    else if (key == "rpmservomax") rpmServoMax = val;
    else if (key == "speedmin") speedInputMin = val;
    else if (key == "speedmax") speedInputMax = val;
    else if (key == "speedservomin") speedServoMin = val;
    else if (key == "speedservomax") speedServoMax = val;
    else if (key == "fuelservomin") fuelServoMin = val;
    else if (key == "fuelservomax") fuelServoMax = val;
    else if (key == "tempservomin") tempServoMin = val;
    else if (key == "tempservomax") tempServoMax = val;
    else Serial.println(F("Unknown set key"));
  }
  else if (word1 == "test") {
    String rest = cmd.substring(firstSpace + 1);
    int sp = rest.indexOf(' ');
    if (sp == -1) { Serial.println(F("Usage: test <rpm|speed|fuel|temp> <value>")); return; }
    String key = rest.substring(0, sp);
    int val = rest.substring(sp + 1).toInt();

    if (key == "rpm") servoRPM.write((int)(safeMapConstrain(val, rpmInputMin, rpmInputMax, rpmServoMin, rpmServoMax) / GEARBOX_RATIO));
    else if (key == "speed") servoSpeed.write((int)(safeMapConstrain(val, speedInputMin, speedInputMax, speedServoMin, speedServoMax) / GEARBOX_RATIO));
    else if (key == "fuel") servoFuel.write(safeMapConstrain(val, 0, MAX_FUEL, fuelServoMin, fuelServoMax));
    else if (key == "temp") servoTemp.write(safeMapConstrain(val, 0, MAX_TEMP, tempServoMin, tempServoMax));
    else Serial.println(F("Unknown test key"));
  }
  else if (word1 == "show") {
    Serial.println(F("Calibration (session):"));
    Serial.print(" RPM input: "); Serial.print(rpmInputMin); Serial.print("-"); Serial.println(rpmInputMax);
    Serial.print(" RPM servo: "); Serial.print(rpmServoMin); Serial.print("-"); Serial.println(rpmServoMax);
    Serial.print(" Speed input: "); Serial.print(speedInputMin); Serial.print("-"); Serial.println(speedInputMax);
    Serial.print(" Speed servo: "); Serial.print(speedServoMin); Serial.print("-"); Serial.println(speedServoMax);
    Serial.print(" Fuel servo: "); Serial.print(fuelServoMin); Serial.print("-"); Serial.println(fuelServoMax);
    Serial.print(" Temp servo: "); Serial.print(tempServoMin); Serial.print("-"); Serial.println(tempServoMax);
  }
  else Serial.println(F("Unknown command"));
}

// --- Main loop ---
void loop() {
  // Handle incoming serial
  if (Serial.available() && Serial.peek() != -1) {
    String s = Serial.readStringUntil('\n');
    s.trim();

    bool numericOnly = true;
    for (uint16_t i=0; i<s.length(); ++i) {
      char c = s.charAt(i);
      if (!(isDigit(c) || c=='-' || c=='+' || c=='.' || c==' ')) { numericOnly = false; break; }
    }

    String low = s; low.toLowerCase();
    if (!numericOnly || low.startsWith("set") || low.startsWith("test") || low.startsWith("show")) {
      handleSerialConsole(s); // Handle console command
    } else {
      // Store telemetry line
      simLines[simIndex++] = s;
      lastSimReceive = millis();

      if (simIndex >= 7) {
        // Parse 7-line telemetry
        int rpm = simLines[0].toInt();
        int speed = simLines[1].toInt();
        int oilTemp = simLines[2].toInt();
        int fuel = simLines[3].toInt();
        int turnLeft = simLines[5].toInt();
        int turnRight = simLines[6].toInt();

        // Map telemetry to servos
        int servoAngRPM   = safeMapConstrain(rpm, rpmInputMin, rpmInputMax, rpmServoMin, rpmServoMax);
        int servoAngSpeed = safeMapConstrain(speed, speedInputMin, speedInputMax, speedServoMin, speedServoMax);
        int servoAngFuel  = safeMapConstrain(fuel, 0, MAX_FUEL, fuelServoMin, fuelServoMax);
        int servoAngTemp  = safeMapConstrain(oilTemp, 0, MAX_TEMP, tempServoMin, tempServoMax);

        servoRPM.write((int)(servoAngRPM / GEARBOX_RATIO));
        servoSpeed.write((int)(servoAngSpeed / GEARBOX_RATIO));
        servoFuel.write(servoAngFuel);
        servoTemp.write(servoAngTemp);

        // Relays for turn signals
        digitalWrite(PIN_RELAY_RIGHT, turnRight ? HIGH : LOW);
        digitalWrite(PIN_RELAY_LEFT,  turnLeft  ? HIGH : LOW);

        // High beam relay
        int hb = readHighBeamState();
        digitalWrite(PIN_RELAY_HIGH, hb ? HIGH : LOW);

        // Relay 4: manual switch
        digitalWrite(PIN_RELAY_CUSTOM, digitalRead(PIN_MANUAL_SWITCH_IN) == LOW ? HIGH : LOW);

        // Keyboard HID for turn signals/high beam
        static int prevTurnL=0, prevTurnR=0, prevHB=0;
        if (turnLeft && !prevTurnL) Keyboard.press(KEY_TURN_LEFT_PRESS);
        if (!turnLeft && prevTurnL) Keyboard.release(KEY_TURN_LEFT_PRESS);
        if (turnRight && !prevTurnR) Keyboard.press(KEY_TURN_RIGHT_PRESS);
        if (!turnRight && prevTurnR) Keyboard.release(KEY_TURN_RIGHT_PRESS);
        if (hb && !prevHB) Keyboard.press(KEY_HIGHBEAM_PRESS);
        if (!hb && prevHB) Keyboard.release(KEY_HIGHBEAM_PRESS);

        prevTurnL = turnLeft;
        prevTurnR = turnRight;
        prevHB = hb;

        simIndex = 0; // Reset telemetry buffer
      }
    }
  }

  // Reset buffer on timeout
  if (simIndex > 0 && (millis() - lastSimReceive > SIM_TIMEOUT_MS)) simIndex = 0;

  // Handle stalk buttons A0
  static bool prevA0minus=false, prevA0plus=false;
  bool curA0minus = readA0_minus();
  bool curA0plus  = readA0_plus();
  if (curA0minus && !prevA0minus) Keyboard.press('z');
  if (!curA0minus && prevA0minus) Keyboard.release('z');
  if (curA0plus && !prevA0plus) Keyboard.press('x');
  if (!curA0plus && prevA0plus) Keyboard.release('x');
  prevA0minus = curA0minus;
  prevA0plus  = curA0plus;

  // Wiper buttons A2
  static int prevWiperA2 = 0;
  int curWiperA2 = readWiperButtonsA2();
  if (curWiperA2 != prevWiperA2) {
    if (prevWiperA2 == 1) Keyboard.release('1');
    if (prevWiperA2 == 2) Keyboard.release('2');
    if (prevWiperA2 == 3) Keyboard.release('3');
    if (curWiperA2 == 1) Keyboard.press('1');
    if (curWiperA2 == 2) Keyboard.press('2');
    if (curWiperA2 == 3) Keyboard.press('3');
  }
  prevWiperA2 = curWiperA2;

  delay(5); // Small delay
}
```

---

## SimHub Setup Guide

This section explains how to configure **SimHub** to send telemetry data to the Arduino dashboard.  
SimHub will output 7 values (RPM, Speed, Temperature, Fuel, Instant Consumption, Turn Indicators Left & Right) through a **Custom Serial Device**, which the Arduino reads in real time to control the servos and relays.

---

### 1. Connect and Detect the Arduino

1. Flash the firmware to your Arduino Pro Micro .  
2. Connect the board to your PC using a USB cable.  
3. Open **SimHub** and go to the **Custom Serial Devices** tab → **Add New Serial Device**.  
4. Check that the board is listed with its COM port.

<img src="https://github.com/Eduard-Alexandru-V/HLR_Car_Driving_Sim/blob/main/images/connecting%20the%20arduino.jpeg?raw=true" width="1000">

---

### 2. Setup the Serial Device

1. Give it a name (for example: `Golf4Dash`).  
2. Set the **Serial Speed** to `115200`.  .  
3. Set **Output Frequency** to `60 Hz`.

   <img src="https://github.com/Eduard-Alexandru-V/HLR_Car_Driving_Sim/blob/main/images/setting%20up%20the%20arduino.jpeg?raw=true" width="1000">

4. In the **Update Messages** box, in the **Computed value**, paste the following:
   
 ```ccp
   
  ''+round([Rpms],0)+'\n'+
  ''+round([SpeedKmh],0)+'\n'+
  ''+round([OilTemperature],0)+'\n'+ 
  ''+round([FuelPercent],0)+'\n'+ 
  ''+round([InstantConsumption_L100KM],0)+'\n'+
  ''+[TurnIndicatorLeft]+'\n'+
  ''+[TurnIndicatorRight]+'\n'
  
 ```

 Explanation for each of the lines:

| Line | Data Type                  | Description                     |
|------|-----------------------------|----------------------------------|
| 1    | RPM                         | Engine RPM                      |
| 2    | SpeedKmh                   | Vehicle speed in km/h           |
| 3    | OilTemperature            | Coolant / oil temperature (°C)  |
| 4    | FuelPercent               | Remaining fuel (%)              |
| 5    | InstantConsumption_L100KM | Live fuel consumption           |
| 6    | TurnIndicatorLeft         | Left blinker state (0 or 1)     |
| 7    | TurnIndicatorRight        | Right blinker state (0 or 1)    |

<img src="https://github.com/Eduard-Alexandru-V/HLR_Car_Driving_Sim/blob/main/images/ncalc%20formula.jpeg?raw=true" width="1000">

---

### 3. Configure the Output Data Format

The firmware expects each telemetry value on a **separate line** and in the **exact order** shown above.  
Do not modify the format or add extra characters.


---

### 4. Enable the Device

1. Tick the checkbox next to your `Golf4Dash` device to enable it.  
2. Click **Save and Restart** SimHub if required.  
3. Launch your game.  
4. SimHub will now stream telemetry to the Arduino.

<img src="https://github.com/Eduard-Alexandru-V/HLR_Car_Driving_Sim/blob/main/images/connect%20the%20serial%20device.jpeg?raw=true" width="1000">

---

### 5. Verify Incoming Data

While SimHub is running, you cannot open the Arduino Serial Monitor because the COM port is already in use.  
To check the data being sent:

1. Go to **Arduino** → **Custom Serial** in SimHub.  
2. Next to your device, click **Log incoming data**.  
3. A new window will display the 7-line telemetry block being sent to the Arduino (When the game is running)  , for example:

```ccp
2431
82
89
43
12
0
1
```  

---

## License

This project is released under the MIT License. It may be modified and adapted for educational or personal use.

---

## Acknowledgements

This documentation was prepared for RoboChallenge. All hardware components are original Volkswagen Golf 4 parts.
