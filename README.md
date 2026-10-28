# ps5pad

Pair and manage PS5 DualSense controllers over Bluetooth on a Raspberry Pi.
One bash script, no dependencies beyond BlueZ (`bluetoothctl`), which Raspberry Pi OS already has.

Should also work with the DualSense Edge and the PS4 DualShock 4 (not tested yet).

## Install

On the Pi:

```bash
sudo install -m 755 ps5pad /usr/local/bin/ps5pad
```

## Commands

| Command | What it does |
| --- | --- |
| `ps5pad pair` | Guided pairing. Start here. Retries up to 3 times. |
| `ps5pad status` | Paired controllers, whether they're connected, and battery |
| `ps5pad doctor` | Checks the Pi's Bluetooth setup and fixes what it can |
| `ps5pad remove AA:BB:CC:DD:EE:FF` | Forget one controller |
| `ps5pad forget-all` | Forget every PlayStation controller |

The script re-runs itself with `sudo` when needed. To scan for longer than 30 seconds: `SCAN_SECS=45 ps5pad pair`.

## Pairing

1. Unplug the controller from USB and make sure it's off. If it's on, hold PS for about 10 seconds.
2. Run `ps5pad pair`.
3. Hold **Create** + **PS** until the light bar flashes quickly in double blinks (3–5 seconds).
   Slow pulsing means it's looking for a PS5 instead. Let go and try again.
4. Press Enter straight away. The light bar goes solid once it's connected.

After that, press PS to reconnect. Hold PS for about 10 seconds to turn the controller off when you're done.

A controller remembers one host at a time. After using it on a PS5 again, run `ps5pad pair` to bring it back to the Pi.

## Lag

The Pi's built-in Bluetooth has a small antenna, and it shares its radio with Wi-Fi. If the controller feels laggy:

- Use Ethernet instead of Wi-Fi, or at least 5 GHz Wi-Fi.
- Keep USB 3 drives and cables away from the Pi.
- Avoid metal cases and closed cabinets.
