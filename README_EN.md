# CAN-RS4  
Control DJI RS4 Gimbal via CAN Communication.

# DJI RS4 Gimbal CAN Control Project

This project enables CAN-based control of the DJI RS4 gimbal.  
It uses Python scripts and a SocketCAN environment to communicate with the gimbal.

---

## 📌 Project Overview

- Controls the DJI RS4 gimbal using CAN communication  
- Analyzes the Lua script used in Mission Planner:  
  [`mount-djirs2-driver.lua`](https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_Scripting/drivers/mount-djirs2-driver.lua)  
- Controls gimbal angles using the `send_gimbal_angle()` Python function  
- The angle transition time is adjustable (default: 2 seconds)

---

## 🧾 CAN Protocol Format

<img src="./images/CAN_Protocol.png" width="500"/>

| Item                  | Value                            |
|-----------------------|----------------------------------|
| CAN ID                | `0x223`                          |
| Transmission Speed    | `1 Mbps`                         |
| Error Detection       | DJI proprietary CRC16 / CRC32    |
| Data Transmission     | 8-byte segmented CAN frames      |

---

## 🔧 Hardware Configuration

<img src="./images/HW_Config.png" width="500"/>

| Component                 | Description                                                        |
|--------------------------|--------------------------------------------------------------------|
| USB-CAN Adapter          | **CANable Nano v1.0**                                               |
| Termination Resistors    | Two 120Ω resistors                                                  |
| Custom Gimbal Connector  | **DIY connector required** (refer to schematic image above)        |
| Cable Connections        | Shared GND, CAN_H, CAN_L                                            |
| Operating System         | Linux (e.g., Ubuntu)                                                |

---

## 🚀 How to Run

1. Connect the CAN adapter to the Linux system and check connection using `lsusb`
2. Enable CAN interface at 1 Mbps:
   ```bash
   sudo ip link set can0 up type can bitrate 1000000
   ```
3. Run the script:
   ```bash
   python3 CAN_Send.py
   ```

---

## 🧰 Technology Stack

- **Physical Layer**: CANable Nano, 120Ω termination resistors  
- **Kernel Layer**: SocketCAN (native Linux CAN interface)  
- **Tool Layer**: `can-utils`, `python-can`  
- **Application Layer**: Python script-based gimbal control  

---

## 🙋 Q&A

For questions or technical inquiries, please contact:

📧 jw6258@sch.ac.kr

---

## 📄 License

This project is based on code licensed under the MIT License.

Portions of this code are derived from:
- [ArduPilot mount-djirs2-driver.lua](https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_Scripting/drivers/mount-djirs2-driver.lua)

```
MIT License

Copyright (c) ArduPilot

Permission is hereby granted, free of charge, to any person obtaining a copy  
of this software and associated documentation files (the “Software”), to deal  
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included  
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL  
THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN  
THE SOFTWARE.
```

Modified and extended by **Jeongwon Choi (2025)** for use with the DJI RS4 Gimbal via CAN communication using Python.
