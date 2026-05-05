# Arduino Biometric Access Control System

> Touch-sensor authentication · DS1307 RTC time logging · 16×2 LCD · Admin menu · EEPROM storage (150 entries)  
> **La Cité collégiale — Embedded Systems · Winter 2025**

---

## Photos

| Full System | Admin Mode on LCD |
|---|---|
| ![System](../images/fingerprint-system.jpg) | ![Admin Mode](../images/fingerprint-system-2.jpg) |

---

## Overview

An **Arduino-based biometric access control system** that authenticates users via a **KY-036 metal touch sensor**, logs each access event (user ID + timestamp) to **Arduino EEPROM** using a **DS1307 real-time clock module**, and displays live status information on a **16×2 I2C LCD**.

The system supports two users, an admin review mode, audio/visual feedback (buzzer + LED), and a 4-button navigation menu. Capacity: up to 150 access log entries.

---

## Features

- ✅ Touch-based user authentication (KY-036)
- 🕐 Real-time timestamp logging via DS1307 RTC module
- 📟 16×2 I2C LCD status display
- 👤 2-user support with Up/Down button switching
- 🔐 Admin mode — review access logs per user
- 🔄 Long-press reset (3 seconds) clears all logs
- 🔔 Active buzzer + red LED feedback on access events
- 💾 EEPROM storage — up to 150 entries

---

## Hardware

| Component | Part | Qty |
|-----------|------|-----|
| Microcontroller | Arduino Uno R3 | 1 |
| Display | 16×2 LCD via I2C module | 1 |
| RTC Module | Elegoo DS1307 (ds1307-module-v03) | 1 |
| Touch Sensor | KY-036 Metal Touch Sensor Module | 1 |
| I2C Interface | I2C module (LCD backpack) | 1 |
| Push-buttons | Tactile switches | 4 |
| Buzzer | Active buzzer 5V | 1 |
| LED | Red LED | 1 |

---

## System Modes

### Logging Mode (default)
- System waits for touch sensor input
- On valid touch: reads current time from RTC, stores `{UserID, HH:MM}` to EEPROM
- LCD displays: `Time: HH:MM` / `User: X`
- Red LED flashes + buzzer beeps to confirm access
- Up/Down buttons switch between User 1 and User 2

### Admin Mode
- Activated via MENU button
- Up/Down buttons scroll through users
- SELECT button displays stored access log for selected user
- Long-press SELECT (3 seconds) → full EEPROM reset

---

## Button Map

| Button | Function |
|--------|----------|
| MENU | Enter / exit admin mode |
| UP | Next user / scroll up in log |
| DOWN | Previous user / scroll down in log |
| SELECT | View user log / long-press to reset |

---

## Wiring Overview

```
Arduino Uno R3
├── A4 (SDA) ─── I2C bus ─── [LCD I2C module] + [DS1307 RTC]
├── A5 (SCL) ─── I2C bus ─── [LCD I2C module] + [DS1307 RTC]
├── D2 ──────── KY-036 touch sensor (digital output)
├── D3 ──────── MENU button
├── D4 ──────── UP button
├── D5 ──────── DOWN button
├── D6 ──────── SELECT button
├── D7 ──────── Active buzzer
├── D8 ──────── Red LED (+ 220Ω resistor)
├── 5V ──────── VCC rails
└── GND ─────── GND rails
```

> I2C was chosen for the LCD and RTC to minimise Arduino pin usage — both share the same SDA/SCL bus.

---

## Code

The full Arduino sketch is available here:  
🔗 [https://pastebin.com/aRLB4ggq](https://pastebin.com/aRLB4ggq)

**Libraries used:**
- `Wire.h` — I2C communication
- `LiquidCrystal_I2C.h` — LCD via I2C
- `RTClib.h` — DS1307 RTC
- `EEPROM.h` — built-in Arduino EEPROM read/write

---

## Schematic

Designed in **Tinkercad Circuits** — full schematic and breadboard view available in the project presentation.

---

## Problems Encountered & Solutions

| Problem | Cause | Solution |
|---------|-------|---------|
| Upload failures | Arduino Nano USB/bootloader issues | Switched to Arduino Uno R3 |
| Compilation errors | Library version conflicts | Updated libraries, resolved header conflicts |
| First RTC not working | Defective DS1307 module | Replaced with new module |
| Small touch area | KY-036 sensitivity limitation | Proposed upgrade: fingerprint sensor module |
| EEPROM saturated at 105 entries | Arduino built-in EEPROM limited to 1 KB | Proposed upgrade: external I2C EEPROM module |

---

## Future Improvements

- Replace KY-036 touch sensor with a **fingerprint sensor** for true biometric authentication
- Add **external I2C EEPROM** (e.g. AT24C256) to expand log capacity beyond 150 entries
- Upgrade to a **larger LCD or OLED** for viewing more log entries at once
- Improve breadboard wiring to a proper PCB

---

## Skills Demonstrated

`Arduino Uno` `C/C++ embedded programming` `I2C protocol` `DS1307 RTC` `EEPROM storage` `LCD interface` `Touch sensor` `Software debouncing` `Menu-driven UI` `Tinkercad schematic` `Sensor integration` `System design`

---

*Adam Zaghloul · La Cité collégiale · Winter 2025 · [adamzaghloul07@gmail.com](mailto:adamzaghloul07@gmail.com)*
