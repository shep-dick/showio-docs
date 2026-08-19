# Changelog

## Firmware Release - Version: 0.3.1
Released August 19, 2026

### Fixes:

- No longer crashes on boot in DHCP mode

## Firmware Release - Version: 0.3.0
Released August 12, 2026

### Features:

- Fully-featured web UI
- Cloud firmware updates
- OSC WebSocket integration

### Improvements:

- Efficiency improvements to network message piping 
- Improve reliability of configuration system

### Fixes:

- Updated [sio/cfg/osc/reportMsg/di/<channel>/<state>] response address to include channel and state
- Changed default device name to "My ShowIO" (was SHOWIO_PROTO5)
- Changed USB interface product name to "SIO-S08DC" (was SIO-PROTO5)

## Firmware Release - v0.2.7
Released January 30, 2026

### Features:

- Enabled Watchdog timer in firmware; if program crashes, watchdog will auto-reset

### Fixes:

- Stopped firmware + bootloader version from getting overwritten on factory reset

## Firmware Release - v0.2.6
Released January 26, 2026

### Features:

- Added ability to factory reset nodes using 10th dip switch
- Added channel configuration settings
    - Software-set debouncing filter

### Fixes:

- Eliminated crash points when pinging a node with /ping
- Fixed /sio/cfg/lan/get response address

### Changes:

- Changed serial number format to new 18-char format