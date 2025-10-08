# HLR Car Driving Simulator 

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
| Arduino Pro Micro  | Microcontroller that reads the stalk inputs, controls the servos, and communicates with SimHub over USB. | ![Arduino](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSl6x2KCtAm-P8l4KiwnmfnWbZx0AuECHsDmQ&s) |
| Golf 4 Instrument Cluster Shell | Original dashboard housing; holds the servos and gearboxes, preserving the original look. | ![Cluster](https://www.utilinx.pt/zArchives/Products/1161/Photos/img-20190409-143035.jpg) |
| Golf 4 Turn Signal Stalk | Provides left/right indicators and +/- buttons; input read via resistor ladder. | ![TurnStalk](https://i.ebayimg.com/images/g/FucAAOSwD4Zmi~25/s-l1200.jpg) |
| Golf 4 Wiper Stalk | Provides OK / UP / DOWN buttons and 4-step rotary switch; input read via resistor ladder. | ![WiperStalk](https://assets.globalparts.co.uk/assets/jpg/1k0953519l_3/windscreen-wiper-stalk-control-switch-vw-volkswagen-golf-5-sku-1k0953519l-photo-3.webp) |
| Standard Hobby Servos (x4) | Drives the speedometer, tachometer, fuel, and temperature gauges via 3D-printed gearboxes. | ![Servo](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSMCMmdtN2k7aqllpJNSOEfjLBBtkQdxvOrlw&s) |
| Custom 3D-Printed Gearboxes | Converts servo rotation to the original gauge needle movement; fits inside the cluster shell. | ![Gearbox](path/to/gearbox.jpg) |
| Resistors for Ladder Circuits | Used to differentiate multiple switch positions on single analog lines. | ![Resistors](path/to/resistors.jpg) |
| USB Cable | Provides power and allows the Arduino to act as a joystick + serial device for SimHub. | ![USB](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMHEhUTExMWFhUXFRcXFxgWGRcYGhUZFxUWGhYYGhsaHSghGholHBcVITEiJykrLy4uFyAzODMsNygtLisBCgoKDg0OGxAQGy0mICUrLS0wLS0tLS0tLS01LS0tLS0tLS0xNS0tLS0rLS0tLSs1LS0tKy0tLS0tLS0tLSstLf/AABEIAOEA4QMBIgACEQEDEQH/xAAcAAEAAwADAQEAAAAAAAAAAAAABQYHAgMEAQj/xABJEAABAwICBgYGCAMGBAcAAAABAAIDBBEFIQYSMUFRYQcTcYGRoSIyQlJisRQVI0NygpLRM6LBJFOTssLhVNLT8CU0Y3ODlLP/xAAYAQEAAwEAAAAAAAAAAAAAAAAAAQIDBP/EACcRAQEBAAEDBAEEAwEAAAAAAAABAhEDEiETMUFRcSIyYZFCUmIj/9oADAMBAAIRAxEAPwDcUREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERARF8Jsg+ousztHtN8Qvola7Y4eIQc0REBERAREQEREBERAREQEREBERAREQEReLFcWhwhmvM8NG4b3cgNpSTke1eesrY6FutLI1g4uIHhfasw0l6THkEQ2hZ7zrF57Bsb59qo8tXPih13EgH7yUlzndgOfits9G33ZXqz4a9ifSNSUd9TWlPEDVb4uz8AVXarpJqJ/4UUcbeLruPibA+CzmWtiozld7+J9J1+Q2DuXOCKSt9KZ5iZuAAL3eJAYOeZ5LadLMZ3qaq1VentV7VSRya1g89W6iXae1E7tVk873e6xzifBqjvpNFQbIWyOt60xMx/SbR/wAi7JNMZ2t1WFzGcGWiZ4N1WqeJPiI835r1VuN4m5us+KsDeMgmaP5rKJdX1c33Tj2ryz6SPdmXtB431j5XXmdj73fe+AP9bJNSfKe2/SRM1X/deS4/Sqpm2I+B/ZR7ccf/AHjv0/7r0xY1J/eDvBU90+0dt+nvg0kqKT2ZGfhc5vyKnqTpCqqLV1pJWA7OtbrBw5F4zHYVAUuMSTEN1WvJyAG88M1PUOPy4MdRzZIQ7bHKw9W7j6DxY9oSyUlsW7COk10lusjZIOMZ1XeBuCe8K54RpPTYtYMks8+w/wBF3dud3ErLA3D8Wzkp+pcfvaM6luZiN2ntzKVOi1RAzraaRtbANuoNWZn4ozmSMthv8IWWsZ/DSb1+W2Isk0Z06lovRcTNGDYtd/EZbaATnlwdwtcLUMLxKPFYxJE4OafEHeCNx5LHWLlpnUr1oiKiwiIgIiICIiAiIgIirWmukgwKLVZ/FePR+Ee8f6c+xTJbeIi3ic1w0v0vZgYLGWfMRs3M5u58vlvyiaeo0ie+QvuAbSTSZRx7w0WHpOtsY0X5AZryde2seTK8kXu4NP2kpOeqCb6o3uednMkA8cZxvVaG2a1rBZkbMmRg7bDnvJu5x2krqzmZ9nPrV17vlY2noMwC9w+8ktrE/C0HVYOQueLio1ssuL5g6kfvHa78I39uxdVDRnET1s3qey0+1zPwq/aJaFyaSWkkvFSjZbJ0ttzfdZ8XhxFrqSc1Elt4VLDaJ8zjHSQPlf7TmguI5udsaPAKzUPRbX4jnPIyEcCS9w7m5H9QWxYZhsWExiKGNsbBuaPMnaTzOa9aw11rfZtnpye7NsP6HqWHOWeaQ8GasTfIF/8AMrBRdHeGUeykjceMutKT+slWlFlzV+HggwWmpsmU8LfwxsHyC7jh8R+6j/S39l6UUJRVVo1R1fr0kDu2Jl/GygMS6LcNrb6sLojxieR/Kbt8ldEUy2I4Y1jHQ/NT3NNM2Ue5INR3YHDInt1VX4qms0dP0eUEM309S3XicPhvkO1hHav0KvJieGxYqwxzRtew7nDZzB2g8wtJ1b7VS4+mEMpWV7r0t4Z/+Ge7J/8A7EhycfgfY8CV34NjL6V+sxzopWnVORBuNrHtPyIU7pdoG7CQZIrywDMg5yQjj8TRx2jfxVekP1pqtkcOvsBDOTYTgerDOeO5shzBsDlmNs3mePZlZ5XN1LBpsCRq09e0X1h6swHEe0P5m8xtgcJxKo0ZqHAtLZGkCWIn0ZG7iDv4hw/cKMw+qc0ixcyRjsr5OY9psWnmDdX2qgbpzSdYwBtZBlw1jt1D8D7G3A9huv6fwmefyumE4lHi0TZYzdrvFp3tI3EL2LItB8e+qJwHXEUp1Xg5dW/YHEHZY5Hl2LXVz7x21tjXdBERUWEREBERAREQcZHiMEk2ABJPADasG0yxh2ISvkN8z6I4DY1vh5rXtMq9tHTPbrWfINVo3kG2v3BpPlxWF4syRwke1pLYxrPO5oJDW3PEkgAfsV0dGcS1j1b5kR8TvoYI2yOzceCnYtEuppxU1dwZcoIdhItcyyfCBaw3ktvYZHu6M9Hfruqb1o1mMHWyX2Gx9BnYTnzDSp3pCxE11W9ozbHaJoG8jN+XHWNvyhXt51wrPE5cNCNGhpBNeQf2eK2sPfdtbH2WzPcN62JjQwAAAACwAyAA2AKN0awoYLTRwjaBd54vObz4+QClFz713VtjPbBERUWEREBERAREQEREBZb0gaJtobzRt+xebPaNkbjscODSfA9uWpLqqqdtWx0bxdrgWuHEEWKtjXbeVdZ7o/Pb6g6wLz6Y1WPJ9tuyKQ8XDJjjvuw7dYq0aK4r9U1UbybMf9nJws45O7jY9l+Kr2mGFOw90kd/SjcQDxG1h7wQUo5vpcLXcRf9wuziWcObmyrR0h4SKCqLmj0Khpf2SNsJPG7Xdrir9oXiRxSkjeTd7RqP/EzK55kWPeqxpXJ9Z4ZSznNzXR6x5lro3/zW8F29FE/o1EfBzHj8wc0/5AsNeen+G08b/K/IiLBqIiICIiAovGcfgwhri97dYC+oCNY32C266+aSY03BIi82LzkxvE8TyG//AHWFaRYs6cuc513OJJJ3neVr0+n3eaz3vjxElUY9NpDWlxBcA1xdq5hjAPJoJAvxPNR+NTOijlhGyV8Rd2RlxA8XDwWj9FeAdXh7zLFqPqda7j6zoyLMJ4DNxA533qlY3QOaXNcPTYS1w5g7ezet8amuYy1mzyuvQ5SiKmml3ul1b/CxjbebnKpYAPrWugJ+8nMp5+kZT8lcui93/h0oG1sso79Rp/qqpoAP7dS9j/8A8ZFSe+qtfbLZ0RFzNxERAREQEREBERAREQEREGV9LEAZNre9CL9rXOHysqdhlP8ARYWjc4a4/Nt8HBw7lcOl+otK1vCIeLnuy8gqg2R0MLGvObGao5Zk28XFdvT/AGxy796vk4tgTL75Bb/7RPyuuXRSPtKk/DH5uk/ZR+MYiH4XQxj2gXnsju3Ptc4HuU90VU2pDNJ78gaOYY393nwWV/Zf5rSfvn4XhERc7YREQFXtItLIsGOoB1kvug2Db7NY7uweS7dK8eGCRZWMrrhg4cXHkPNZQ+YzEvcbkkkk7ydpW3T6fd5rPe+PEdmkmKS4sTJI4XtYAbGjgAvnR9og7SKfrp2/2eI7N0rxsb+EZE9w35QuJVlgTuGzmtU6JsLlw+jL5bgzSda1p9lpa0AngTa/ZZadW9ueIzxOdc1dQLKk9IWC3H0qMZtAErfebkGuHMZDmOxXddFfStro3xO9V7HNPY4Wv2rnzrtvLfU5nDMdDsfbgpc1wvBIbuIzLDa2tbeLWuNuWXAweis4oaunN7hsvV34hxLL9lnXXgq2vw17muycxxa8biWmxPK+2++/euTntlNjeN4sbHIjeD/W66uJef5c3N/pvyKs4FpjBXhrZD1UlgDrZNcd+q7Z3GxVmBuuSyz3dMsvsIiKEiIiAiIgIiICIiAvhOrmVH4vjkGDi8rwDuaM3HsaPnsWa6VacvxAFjfsot4v6Tx8R4ch4lXz07pTW5EXpNXjFqmSb2db0L+60WafAX71X8TLtTXIIYW3YT7eZaXDlcOHcrZoRosdKD10120zXW1Rk6YjaL7mDYTt2jLaufSdE2WrbE0AMjhjbqgWAALyGgbhYhdU3Oe2MLm8d1VuGpfJDEHfdx6jQOGs53iS8+S3DRjDfqmliiPrBt3/AI3ek/zJHcs20AwX63qRI4fYwEOPB0m1je71j2DitdWHW18Rr0580REWLUXkxXEWYXE6V5yGwb3Hc0cyvWsZ0x0xGKTuZZ/VxOc1osMyDZzjntNu4d6vjPdVdXiOrFcQfi0rpHk3PDY1u5ovuCh66p3DYNq65sZZa2bd13DJMGwmTSWobTxZD1pH7mMG139AN5IXXzJHPxbUv0faMHSefrpW/wBmidsOyR4zDOwZE9w3rcBkvJhWHR4TEyGJuqxgsB8yeJJuSea9a4967q6M54giIqrM26T8D6twqmj0X2ZLydsY/v8AVP5VWL/XNIYXC9RSgvjPtSwD14wdpcz1gOAsN62qspWVrHRyNDmPBa4HeCsYx3CJdG6gNDiHNOvBL7wGwHdrDYRv7Ct+nrmcMdzi8q9TyStLQw9YHEADK5vsHeprD9KqjBXdXrSQkbY3g2H5HDLwCj8Q1CTI1oa1x+1jGyF5OZb/AOi47PdJ1T7JN40Z0igxVjaXEGMk3RySAOB4NcTsdwdv357dNXx7KZnn3d+G9JBNutja74o3ap/Sb38QrBS6cUc+1zozwe0/Ntx5qKxLosoqnOIywH4HazfB9z4EKuVnRXWQfwKuN/ASNdH5jXWX/nf4afrjTIMdpqj1aiI8tdoPgTde6OVsmwg9hBWHVGhmL0uyBsg4skj/ANTmnyXjkwXFINtDJ+UB3+UlPTx/snv19P0AuLnhu0gdq/PZpsT/AOCqf8KT9l9bheJy7KGbvYR/msnp5/2O+/TepsUgg9aaNva9o+ZUdU6XUdNtnafwBz/8ossei0Vxeo2Ujm83Pib833UjT9GmJ1PryQRjfd7nHwayx8U7MT3qO7f0udf0kwQ/w4nO5vIYPK5+SqWM9JM9RcCQRjhHkf1G58LL7UaC0eCZ11c+R23qoQGk8jcuIHM6qruK4tS0oLaanZE33nXkld2vfcjsbbvWmc5+Irq6+a8c2JyVN3AEXzLn3z555le7RHRmXS2azS4QtP2s3D4Gbtc+W3kZXRTQGp0kIlqdaCn22OUko+EH1W8z3A7VecV0nptF4hTUbGlzBYBvqRneXH2nX2jbe9yE1vnxkznjzpK4zi0GiFOyONouG6sUQ4DeeDeJ39pWO4xij6t7nudrSPN3Hh3bgBkByXKsrJsXfK8EyPax0ksh9WNjQSSTsAsCA0dgC4aB4Y7FqqEP9qQEj4G+k4d4bbvTOZiI1bqt1wDDGYPBHFGLANF+LnHNzid5JUgiLldAiIg4TSdUL+XFVyTAqeUue+CO5LnuIba5cbuJI25qT0hwKHSKEwztLmXDvRcWkEbCC03G/wAVXW9GFCxwc0zNIN8pLZ2tw4eee3NReUxF6S6HDSWMxUrIohHIC57gRdwvdgIBJtlrczb2Tez6D6Ks0Vg6sEPkcbyPtbWO4D4WjId53qdpadtIxrGCzWiwH/e0812qZ4nCKIiICIiAo7HcGixyIxSjLa1w9ZjtzmnipFEGG6Q4HJgj+rnGRuI5h6rxwPA22tPmM1XzHJQ7Brx8N47OXJfouto469hjlYHsdta4XB/35rN8f6OZaW76J+s3+5kOY5Nccj2G3aV0Y6s+WGun9InRfTuXDQGX66MZajyQ9nJp2gcjccLLRMK0zpMRsOsEbvdl9DzPonuKxOuYKd+pURPhkG5wLT2jlzC4iMu9SUO5OzV70868om7H6NY8PFwQRxGa5L84xvqaXNmX4HFpXN+N1zfan/xT/wAyz9C/a3q/w/RTjq5lRVdpLSUF9eojuNzTrHwbcr8+VFbVVPrNe78Tr/MrhBQz1R9JzYxxfrHyYCp9H7p6l+Gv4n0oU9PcRMc88XEMH9T5BUbHukyprbta/q2nLVjyJ/NfW81GU+DUcGc888x92NrIWn8znOcR+UKVptKKbAv/AClLBC733Xml/W7Z8laYk9p/aLrn3ryYPofiOkZ1urMMZzMk129pDfWd22tzVsw7DcK0N9NzvpdSPaycGn4R6jM+JLgqXW6WVWPu1AZp3H2Ggkf4bBbyUxhPR3iOL2MxbTM+L0n25MabDvITX/VJ/wAx3aT9IUteC3WEUfuMOZ/E/aewWHauvRvQmr0is+QGnp+LhaR4+Bh2D4ndwK0PRrQCjwAh4YZZR95LZxB+Eeq3tAvzVlqp20rHPcbNa0uJ4AC5Wd6vHjMWmPnTP9OqSDR+gbR07Q3rXt17Zuc1vpOc47SSQxue4kbMl0dFOHXkkmtkxojb+J1i7vAA/UqlX1bq6R8r/WkcXnlfYOwCw7lo/RY5zqR1wA3rnaptYuFm3J453F+XJX3O3HCM/q3yuSIi5mwiIgIiICIiAiIgIiICIiAiIg89dQxYg3UljZI3g9ocPNVHEui6grLljZITxiebfpdceFldkUy2eyLJWT1XRHLH/BrstwkYfm139FHy9GOJx+rPTu7XSD/QtoRX9XX2r2ZYkejXFnfeU4/+R/8A012xdFGIS+vVQt/CZHfNoW0Inq6PTyyqj6Gm/fVr3co2Bnm4u+SsmG9GWG0FiYTKRvmcX/y5N8lcUVbvV+VpmR0UdHHQt1Yo2Rt91jQ0eAC70RVS+E6uZ2Kh6daURVMRp4H65cRrub6oaDcgO3kkDZla67OkvFuraymac3enJb3Rk1p7Tc/l5rPQV0dLp/5VlvfxHS5rpTqtF3OIa0DeSbALc8Ew4YTBHCPYaATxO1x7ySe9Ya+TqzcGxGYIyII2EHcVtWida/EKOGWT13Mz52JAd3gA96df4R0ksiIudsIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAuMsgiBc42ABJPAAXJXJVPpFxT6HTiJp9KY2PJgzf45DvKnM5vCLeJyzzGsQOJzSTH2nXA4NGTR4ALwNNhf9/6rk4X2Fdcp3LvniOUpKR2JSxwN9aR4b2AnM9wue5b5TwtpmNY0Wa1oaBwAFgPBZr0U4V18slU4ZM+zj/ERd57hYfmK05cnV1zeG/TnEERFk0EREBERAREQEREBERAREQEREBERAREQEREBERAWPdIFPX4liUkcUZLGRMLCG3BZYXNz8ZcLclsKqeIaY0NFUSxy1LGPj1Wua4OGoLAgk6thcu47NVTNXPmIsl92VPwjEYtsRP5D+yiXV8kUpgljLZDYDIgknZkeO5beNK6Oa7WVcOtkLa4uNbZkc9mY4rjR6HU1XOyumjLp/Rc0OcdWO38Mauy7RYZ3zF1fPW18q3pRK6L4UMFpYod7W3fze7N3mT3AKVRFmuIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgLx1mFQVxvLBFIdl3sa4+JC9iIIYaKULSHCkgBBBFo2DMbNgUyiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiIP//Z) |


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

STL files are included in the `STL/` folder.

---

## License

This project is released under the MIT License. It may be modified and adapted for educational or personal use.

---

## Acknowledgements

This documentation was prepared for RoboChallenge. All hardware components are original Volkswagen Golf 4 parts.
