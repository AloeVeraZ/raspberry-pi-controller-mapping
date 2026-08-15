<div align="center">

# Raspberry Pi Controller Mapping

### Xbox and SCUF input visualization with joystick driven servo control

<img alt="Platform: Raspberry Pi" src="https://img.shields.io/badge/platform-Raspberry_Pi-C51A4A?style=for-the-badge&logo=raspberrypi&logoColor=white&labelColor=8E1334"> <img alt="Language: Python" src="https://img.shields.io/badge/language-Python-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=255986"> <img alt="Input: Xbox and SCUF" src="https://img.shields.io/badge/input-Xbox_%2F_SCUF-107C10?style=for-the-badge&labelColor=0B5A0B"> <img alt="Output: GPIO 17 servo" src="https://img.shields.io/badge/output-GPIO_17_servo-F59E0B?style=for-the-badge&labelColor=B45309">

Two Python prototypes for inspecting a game controller and mapping the left stick heading to a positional servo on a Raspberry Pi.

[Overview](#overview) · [Controller map](#controller-map) · [Servo behavior](#servo-behavior) · [Setup](#hardware-and-software)

</div>

---

## Overview

This repository contains a visual controller diagnostic and a Raspberry Pi servo experiment. The visualizer displays live axes, buttons, triggers, and D pad input. The servo script reads both left stick axes, converts the full joystick heading to a 0 to 180 degree servo command, and drives a servo from GPIO 17 through `pigpio`.

## Project files

| File | Purpose |
| --- | --- |
| [`scuff_controller_visual`](scuff_controller_visual) | Pygame based Xbox and SCUF controller visualizer |
| [`servo movement based on controller`](servo%20movement%20based%20on%20controller) | Left stick heading to servo control for Raspberry Pi GPIO 17 |

## Controller map

| Control | Index or axis |
| --- | ---: |
| A, B, X, Y | 0, 1, 3, 4 |
| LB, RB | 6, 7 |
| Guide | 8 |
| View, Menu | 10, 11 |
| L3, R3 | 13, 14 |
| Left stick X, Y | axes 0, 1 |
| Right stick X, Y | axes 2, 3 |
| Right trigger, Left trigger | axes 4, 5 |
| D pad | hat 0 |

## Servo behavior

The servo prototype uses BCM GPIO 17 and maps the left stick heading around a full circle to a 0 to 180 degree servo sweep. The current configuration uses a 500 to 2500 microsecond pulse range, a `0.10` stick dead zone, and smoothing to reduce abrupt movement.

> [!CAUTION]
> Confirm the servo pulse range, mechanical limits, wiring, and external power supply before connecting hardware. Do not power a high current servo directly from a Raspberry Pi GPIO pin.

## Hardware and software

- Raspberry Pi with Python 3
- Xbox or SCUF compatible controller
- Positional hobby servo
- Appropriate external servo power and a shared ground
- `pygame` and `pigpio`

Install the packages and enable the daemon:

```bash
sudo apt-get install pigpio
sudo systemctl enable --now pigpiod
python3 -m pip install pygame pigpio
```

## Run

The files do not currently use `.py` extensions, so pass them directly to Python:

```bash
python3 scuff_controller_visual
python3 "servo movement based on controller"
```

The servo script currently searches for a companion file named `controller mapping.py`, while the committed visualizer is named `scuff_controller_visual`. Run the visualizer separately as shown above, or set `MAPPING_PATH` to its full path before starting the servo script.

---

<div align="center">

Controller and servo experiments by **[Angelo Demetroulakos](https://github.com/AloeVeraZ)**

</div>
