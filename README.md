## What It Does
Scans all 13 WiFi channels and watches for **deauthentication (0xA0)** and **disassociation (0xC0)** frames. When the packet rate stays high, the LED turns on to indicate an attack.

## Hardware Required
- ESP32 board (with built-in LED on GPIO 1, or wire an external LED to GPIO 1)
- USB cable

## Setup Steps
1. **Download the firmware and flash, flash offset address is `0x0`**
   - https://github.com/xiv3r/esp32-jammer-detector/raw/refs/heads/main/esp32-firmware-0x0.bin
   
2. **Run**
     - The device starts scanning automatically. No configuration needed.

## How to Read the LED
- **LED OFF** — normal traffic, no attack detected.
- **LED ON** — deauth/disassociation flood detected on the channel being scanned.

## Tuning (optional, at top of sketch)

| Constant | Default | Meaning |
|----------|---------|---------|
| `CH_TIME` | `140` ms | Time spent on each channel |
| `PKT_RATE` | `5` | Packets per full scan cycle to count as "attack traffic" |
| `PKT_TIME` | `1` | Consecutive cycles needed to trigger the LED |
| `LED_INVERT` | `true` | Set to `false` if your LED is active-high |
| `channels[]` | 1–13 | Edit to restrict to fewer channels (faster scan) |

## Notes
- This is a **passive monitor** — it does not transmit or jam anything.
- Reception range is limited by the ESP32's antenna (a few meters indoors).
- Only detects deauth/disassoc frame *types*, not which network they target.
