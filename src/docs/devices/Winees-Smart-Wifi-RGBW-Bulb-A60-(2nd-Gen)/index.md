---
title: Winees Smart WiFi RGBW Bulb A60 (2nd Gen) (WS010078261)
date-published: 2025-06-27
type: light
standard: eu
board: bk72xx
---

https://www.google.com/search?q=Winees+Smart+WiFi+RGBW+Bulb+A60+(2nd+Gen)

This device uses a Leedarson module with BK7231U compatible C-Chip CC8000, see https://www.elektroda.com/rtvforum/viewtopic.php?p=21025914#21025914,
and a BP1658CJ LED driver chip.
For now it can be flashed with a user created ESPHome image built from a configuration with platformio_options as listed below.
For initial flashing (over UART, TX0/RX0) I used uartprogram from https://github.com/OpenBekenIOT/hid_download_py.
Updates can be flashed using ESPHome OTA.

## Configuration

```yaml
substitutions:
  ...

esphome:
  name: "${name}"
  area: "${area}"
  friendly_name: "${friendly_name}"
  platformio_options:
    board_build.bkcrypt_coeffs: "00000000000000000000000000000000"
    board_build.bkboot_version: "1.0.6-bk7231u"
    board_build.mcu: "bk7231u"
    board_flash.calibration: "0x10000+0x1000"

bk72xx:
  board: generic-bk7231t-qfn32-tuya

...

bp1658cj:
   data_pin: P21   
   clock_pin: P20

output:
  - platform: bp1658cj
    channel: 0
    id: blue
  - platform: bp1658cj
    channel: 1
    id: red
  - platform: bp1658cj
    channel: 2
    id: green
  - platform: bp1658cj
    channel: 3
    id: white

light:
  - platform: rgbw
    red: red
    green: green
    blue: blue
    white: white
    color_interlock: true
```
