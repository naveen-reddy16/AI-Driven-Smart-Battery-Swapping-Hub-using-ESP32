# AI-Enabled-Battery-Swapping-Hub-Using-ESP32
A smart AI-enabled battery swapping hub for electric vehicles using  ESP32, featuring NFC authentication, Firebase cloud sync, servo-based ejection, and ML-based battery health prediction.


## 🧠 Overview

Electric vehicle charging downtime is a major challenge in sustainable transportation.  
This project presents a *smart battery swapping hub* that allows users to instantly replace discharged batteries with charged ones — safely, efficiently, and securely.

The system combines:
- ⚙ *STM32* for control logic and sensor management  
- 🌐 *ESP32* for Wi-Fi and cloud connectivity  
- 🪪 *NFC authentication* for secure user access  
- 🤖 *AI model* for battery health prediction  
- 🔄 *Servo-based auto-ejection* for smooth mechanical release  

---

## 🎯 Objectives

- Automate *battery exchange* for e-bikes and EVs  
- Authenticate users through *NFC + Cloud UID verification*  
- Monitor *voltage, current, temperature, and cycles* per battery  
- Log all data to *Firebase Realtime Database*  
- Predict *battery health & remaining life* using *TinyML*  
- Ensure *safety* through environmental and electrical monitoring  

---

## 🧩 Hardware Components

| Component | Quantity | Function |
|------------|-----------|-----------|
| *STM32F103C8T6* | 1 | Controls sensors, relays, and servos |
| *ESP32* | 1 | Manages Wi-Fi, cloud, and ML functions |
| *PN532 NFC Module* | 1 | Secure user authentication |
| *18650 Battery Slots* | 4 | Rechargeable battery packs |
| *Current Sensor (ACS712 / INA219)* | 4 | Measures current for each slot |
| *Temperature Sensor (DS18B20)* | 4 | Monitors battery temperature |
| *Servo Motor (SG90)* | 4 | Ejects batteries automatically |
| *Relay Module (8-Channel)* | 1 | Controls charging power routing |
| *Gas Sensor (MQ-2)* | 1 | Detects overheating or leakage |
| *TFT Display (2.4")* | 1 | Displays slot data and alerts |
| *RTC (DS3231)* | 1 | Logs charge/discharge events with timestamps |
| *Power Supply (12V → 5V)* | 1 | Regulates voltage for components |

---

## 🔒 Authentication Flow (NFC + Firebase)

1. User taps their *NFC card*.  
2. ESP32 reads the *UID* and verifies it in *Firebase*.  
3. Access granted only if UID is registered.  
4. STM32 unlocks or ejects the corresponding slot.  
5. Unauthorized attempts are logged to Firebase.

---

## 🧠 AI-Based Battery Health Prediction

An *on-device TensorFlow Lite model* on ESP32 predicts the *health status* of each battery pack by analyzing:
- Voltage & current patterns  
- Temperature variations  
- Charge/discharge cycles  

*Prediction Output:*
| Status | Meaning |
|--------|----------|
| 🟢 Good | Battery performing optimally |
| 🟡 Degraded | Reduced efficiency detected |
| 🔴 Critical | Needs maintenance or replacement |

This AI-powered insight helps reduce downtime and improve reliability.

---

## 🔄 Battery Swapping Process

| Step | Description |
|------|--------------|
| 1️⃣ | User scans NFC tag for authentication |
| 2️⃣ | Firebase verifies the user |
| 3️⃣ | STM32 checks slot availability |
| 4️⃣ | Servo ejects charged battery |
| 5️⃣ | Firebase logs user ID, slot number, and timestamp |
| 6️⃣ | Sensors ensure safety during the swap |

---

## 🌐 Firebase Cloud Integration

*Realtime Database Example:*
```json
{
  "Slot1": {"voltage": 12.4, "current": 1.2, "temp": 29.8, "status": "Ready"},
  "Slot2": {"voltage": 11.1, "status": "Charging"},
  "Slot3": {"voltage": 0.0, "status": "Empty"},
  "Slot4": {"voltage": 12.6, "status": "Ready"},
  "user_uid": "A1B2C3D4",
  "timestamp": "2025-10-29T12:30:45"
}
