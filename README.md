# ⚡ User-Interactive STM32 Closed-Loop V/f Induction Motor Control

A production-grade **industrial motor control and telemetry platform** combining real-time embedded control with a modern web-based dashboard.

🔗 **Live Dashboard:** https://speedcontrol.vercel.app/

---

## 🚀 Project Overview

This system implements a **Closed-Loop Variable Frequency Drive (VFD)** for a three-phase induction motor using **scalar V/f control** with feedback regulation.

The controller dynamically adjusts frequency while maintaining a constant **V/f ratio**, ensuring:

* Constant air-gap flux
* Stable torque across speed range
* Efficient operation from **0–1500 RPM**

---

## 🎯 Key Highlights

* 🔁 **Closed-Loop Speed Control** using PI controller
* ⚡ **10 kHz SPWM Generation** with dead-time insertion
* 🧠 **Real-Time Telemetry Dashboard** (React + Web Serial API)
* 🛑 **Hardware-Level Safety Protections**
* 📊 **Live Monitoring of Voltage, Current, Speed & Frequency**

---

## 🧱 System Architecture

```text
STM32 (Control + PWM)
        ↓ UART (230400 baud)
Web Browser (Web Serial API)
        ↓
React Dashboard (Vite + Tailwind)
        ↓
Hosted on Vercel
```

---

## ⚙️ Hardware Specifications

### 🧠 Control Unit

* **Microcontroller:** STM32F401RE (ARM Cortex-M4 @ 84 MHz)
* **PWM:** 10 kHz SPWM via TIM1 (Advanced Timer)
* **Communication:** UART @ 230400 baud

### 🔌 Power Stage

* **Topology:** 3-Phase Voltage Source Inverter (VSI)
* **Switches:** IRFP460N MOSFETs
* **Motor:**

  * 0.75 kW
  * 415 V
  * 1.9 A
  * 4-pole (1440 RPM base)

### 📡 Sensing & Feedback

* **Current Sensor:** ACS712 (Hall-effect)
* **Voltage Sensor:** ZMPT101B (RMS sensing)
* **Speed Sensor:** Inductive Proximity Sensor

---

## 🧠 Control Strategy

### ⚡ V/f Control Principle

Maintains:
[
\frac{V}{f} = \text{constant}
]

Ensures:

* Constant magnetic flux
* Torque stability across varying speeds

---

### 🔁 Closed-Loop PI Control

* Eliminates steady-state error
* Adjusts frequency dynamically based on RPM feedback

---

### 🧪 Signal Conditioning

* **EMA Filtering** applied to RPM
* Reduces noise and improves control stability

---

## 🛡️ Safety Features

* ⚠️ **Overcurrent Protection** → Instant PWM shutdown
* ⚡ **Undervoltage Protection** → Prevents unstable operation
* ⛔ **RPM Timeout Detection** → Detects sensor failure
* 🔴 **Emergency Stop (`KILL`)** → Immediate shutdown via UART
* 🔄 **System Reset (`RESET`)**

---

## 💻 Dashboard (Frontend)

Built using:

* **React 19**
* **Vite**
* **Tailwind CSS**
* **Web Serial API**

### Features:

* 🔌 One-click hardware connection (no drivers)
* 📊 Real-time telemetry visualization
* 🎛️ Speed control interface
* 📈 Live parameter updates

---

## 📡 Communication Protocol

### 📥 STM32 → Dashboard

```text
V:xx.xx, I:xx.xx, S:xxxx, F:xx.xx
```

| Parameter | Description    |
| --------- | -------------- |
| V         | RMS Voltage    |
| I         | RMS Current    |
| S         | Speed (RPM)    |
| F         | Frequency (Hz) |

---

### 📤 Dashboard → STM32

| Command     | Function       |
| ----------- | -------------- |
| `S:<value>` | Set speed      |
| `KILL`      | Emergency stop |
| `RESET`     | Reset system   |

---

## 🛠️ Local Setup

### Prerequisites

* Node.js (v18+)
* Chrome / Edge (Web Serial support)
* STM32 Nucleo-F401RE

---

### Installation

```bash
git clone https://github.com/Premchand006/Speed-control.git
cd Speed-control
npm install
npm run dev
```

---

## ☁️ Deployment

This project is deployed using **Vercel**:

* Framework: Vite
* Build Command: `npm run build`
* Output Directory: `dist`

---

## ⚠️ Important Notes

* Web Serial API requires:

  * HTTPS (✔ supported via Vercel)
  * Chrome / Edge browser
* Hardware must be manually connected via browser prompt

---

## 🧠 Learning Outcomes

This project demonstrates:

* Embedded Systems Design (STM32, timers, PWM)
* Power Electronics (VFD, inverter control)
* Control Systems (PI, closed-loop feedback)
* Real-Time Systems Integration
* Frontend Engineering (React + hardware interface)

---

## 📈 Future Improvements

* 🌐 IoT-based control (WiFi instead of UART)
* ☁️ Cloud telemetry logging
* 🤖 Predictive maintenance using ML
* 📊 Advanced analytics dashboard

---

## ⭐ If you like this project

Give it a ⭐ on GitHub and share it!

---
