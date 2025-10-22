# 🔌 Power Outlet Monitor – LED Only (Arduino Nano)

A simple and reliable **power status indicator** built with **Arduino Nano**.  
The project uses two LEDs (red and green) and a button to indicate **power status** and **alarm confirmation** — no display required.

---

## ✨ Features

- 🔴 **Red LED**
  - Starts with fast blinking (~10 Hz) when the system powers on.  
  - Gradually slows down to 1 Hz over the course of one hour.  
  - Indicates an active alarm or unstable power state.

- 🟢 **Green LED**
  - Turns on at a constant brightness when the alarm is confirmed.  
  - Uses PWM pin D10 for adjustable brightness control.

- 🔘 **Button (A2)**
  - Confirms the alarm when pressed (using internal pull-up).  
  - Turns off the red LED and activates the green LED.

---

## ⚙️ Hardware Connections

| Component | Arduino Pin | Function |
|------------|--------------|-----------|
| Red LED    | D11          | Blinking alarm indicator |
| Green LED  | D10 (PWM)    | Constant light after confirmation |
| Internal LED | D13        | Mirrors red LED |
| Button     | A2           | Alarm confirmation (pull-up) |

---

## 💡 Adjustable Parameters

You can easily modify these values in the code:

```cpp
const int GREEN_BRIGHTNESS = 80;   // brightness 0–255
const unsigned long RAMP_DURATION = 3600000UL; // time until slow blink (1 hour)