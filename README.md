# sunwait

[![OpenWrt Compatible](https://img.shields.io/badge/OpenWrt-Compatible-blueviolet)](https://openwrt.org)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-lightgrey)](https://github.com/stangri/sunwait/blob/master/LICENSE)

Small utility for OpenWrt to wait for the sun.

**sunwait** calculates sunrise, sunset, and twilight times (civil, nautical, astronomical), and can optionally wait until a specified solar event before exiting. It's ideal for time-based automation like lighting, irrigation, or camera control on OpenWrt routers and embedded devices.

---

## Usage

```sh
sunwait [options] [sun|civ|naut|astr|angle] [up|down] [+/-offset] [latitude] [longitude]
```

### Modes

- `poll`: Return immediately with success/failure based on whether it's currently after the event
- `wait`: Wait until specified event
- `list [N]`: Show solar events for the next N days (default: 1)
- `report`: Output sunrise/sunset/twilight times for current or specified date

### Options

- `-p`: Print summary of solar times for the date
- `-z`: Use UTC time instead of local
- `-V`: Show version
- `-v`: Verbose output
- `-y YYYY`: Set year (2000–2099)
- `-m MM`: Set month (1–12)
- `-d DD`: Set day (1–31)
- `-h`: Show help

### Twilight Types

- `sun`: Sunrise/sunset (default)
- `civ`: Civil twilight (–6°)
- `naut`: Nautical twilight (–12°)
- `astr`: Astronomical twilight (–18°)
- `angle [degrees]`: Custom twilight angle (negative = below horizon)

### Coordinates and Offset

- Use floating point coordinates with N/S/E/W suffix, e.g. `51.48N 0W`
- `up` or `down` specify rise/set event
- `+10` or `-0:15`: Add/subtract offset from event time

---

## Examples

```sh
sunwait sun up -0:15 51.48N 0W
# Waits until 15 minutes before sunrise in Greenwich

sunwait poll civ down 40.19N 80.79W
# Exits immediately if it's past civil sunset in Pittsburgh

sunwait list 3 naut up 48.5N 123.0W
# List next 3 days of nautical sunrise for Vancouver
```

---

## Why Use sunwait?

- Tiny (~30–50 KB binary)
- No dependencies; pure C
- Compatible with OpenWrt cron/system integration
- Precise and reliable time calculations

---

Project originally developed by [Ralph Campbell](http://www.ralphcampbell.com/sunwait.html).  
This version is maintained for OpenWrt by [Stan Grishin](https://github.com/stangri).
