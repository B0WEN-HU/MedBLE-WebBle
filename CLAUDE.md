# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

WebBle — a single-file static website using the Web Bluetooth API to read BLE sensor data (heart rate) in Chrome.

## Commands

No build step. Serve `index.html` with any static file server, e.g.:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Web Bluetooth requires a **secure context** (HTTPS or localhost). Open in Chrome.

## Architecture

Everything lives in `index.html` — HTML, CSS, and JS are co-located in one file for simplicity.

Key BLE GATT identifiers used:
- Heart Rate Service: `0x180D` (`'heart_rate'`)
- Heart Rate Measurement characteristic: `0x2A37` (`'heart_rate_measurement'`)

Heart rate parsing follows the Bluetooth spec for characteristic 0x2A37:
- Flags byte 0, bit 0: determines if HR value is uint8 (bit=0) or uint16 (bit=1)
- HR value starts at byte 1
