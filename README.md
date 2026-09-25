<div align="center">

<img src="assets/logo.png" width="96" height="96" alt="Ereshkigal">

# Ereshkigal Project

**One-click flashing for the Ereshkigal Wi-Fi security-testing firmware RTL8720DN (BW16).**

No Arduino IDE. No source. No command line. Just this folder.

**English** · [Bahasa Indonesia](README.id.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · [中文](README.zh.md)

![version](https://img.shields.io/badge/version-2.0.0-6c4cf1)
![platform](https://img.shields.io/badge/platform-Windows%2010%2F11-2fa565)
![board](https://img.shields.io/badge/board-RTL8720DN%20(BW16)-14161d)
![languages](https://img.shields.io/badge/UI%20languages-6-e0870b)

</div>

> [!WARNING]
> **Legal & safety notice read before use.**
> Ereshkigal is a Wi-Fi **security-testing** tool. Use it **only**:
> - on networks and devices **you own**, or that you have **explicit written permission** to test;
> - inside a **controlled lab / test environment** you set up for the experiment.
>
> **Do not** use it against networks, devices, or people you are not authorized to
> test. Unauthorized interception or disruption of wireless networks is **illegal
> in most countries** and can lead to **criminal charges**. This project is for
> education, research, CTFs, and authorized penetration testing only. **You alone
> are responsible for how you use it.**

---

<p align="center">
  <img src="assets/screenshot-flasher.png" width="330" alt="Ereshkigal Project (Windows)">
  &nbsp;&nbsp;
  <img src="assets/screenshot-device.png" width="300" alt="Ereshkigal device web UI">
</p>
<p align="center"><sub>Left: the flasher on Windows. Right: the device's built-in web dashboard after flashing.</sub></p>

## What's inside

| File | What it is |
|------|------------|
| **`EreshkigalFlasher.exe`** | The flashing app (Windows, self-contained). |
| **`Ereshkigal.efw`** | The firmware, in Ereshkigal's protected format. |

Distribute the two files together. The app is a small native window in
**English, Bahasa Indonesia, Español, Français, Deutsch and 中文** switch from
the selector at the top right.

## Requirements

- **Windows 10 or 11.** Uses the built-in **WebView2 runtime** (ships with
  Windows 11 and current Windows 10; otherwise install the free *Microsoft Edge
  WebView2 Runtime* once).
- An **RTL8720DN / BW16** board and a **data** USB cable.
- The board's **USB-serial driver** (most BW16 boards use CH340 or CP2102) so it
  shows up as a `COM` port.

## Tutorial flash in 4 steps

1. **Plug in** the board over USB and run **`EreshkigalFlasher.exe`**.
2. `Ereshkigal.efw` is selected for you. Choose your board's **COM port** from the
   drop-down (press the refresh button if it isn't there unplug/replug the board
   and refresh again; the entry that appears is your board).
3. Leave **Speed** at `1500000`.
4. Click **Flash firmware** and wait for **Done**, then power-cycle the board.

Most boards enter flashing mode on their own. **If the log stalls**, do the
on-screen **Download mode** button sequence on the board:

```
   ┌── 1 ──┐      ┌── 2 ──┐      ┌── 3 ──┐
   │ BOOT  │  →   │ RESET │  →   │ BOOT  │
   │ hold  │      │  tap  │      │release│
   └───────┘      └───────┘      └───────┘
   hold BOOT   ·   tap RESET   ·   release BOOT
```

The flasher retries the sync automatically (up to 3×).

## First boot after flashing

1. The device broadcasts an **open** Wi-Fi network named **`Ereshkigal`**.
2. Join it and open **http://192.168.1.1/**.
3. Complete the one-time **setup wizard** set a network name and a password
   (8–63 characters). The device saves it and reboots.
4. Reconnect with your password, reopen **http://192.168.1.1/**, and the full
   dashboard is unlocked.

## Using it for a WPA2 → WPA3 security check

Ereshkigal demonstrates a real, common Wi-Fi weakness: networks on **WPA2 without
Protected Management Frames (PMF / 802.11w)** can be disrupted with spoofed
**deauthentication** frames  anyone nearby can knock clients off, and that forced
disconnect is the first step behind handshake capture and evil-twin attacks.

A typical **authorized** assessment on your own network:

1. **Scan**  open the dashboard, tap *Scan*, select your target network.
2. **Users**  list the devices connected to it.
3. **Attack**  run a *deauth* test and watch your own client(s).
4. **Detector**  dedicate the radio to spotting deauth frames in the air.

**Reading the result**
- Clients **drop off** → the network is WPA/WPA2 without enforced PMF and is
  vulnerable to management-frame spoofing (deauth denial-of-service, and the
  disconnect-then-capture chain that follows).
- Clients **stay connected** → management frames are protected.

**The fix  move to WPA3.** Switch the network to **WPA3 (SAE)**, or at minimum
**WPA2 with PMF set to _required_** (802.11w). WPA3 mandates protected management
frames, so spoofed deauth/disassociation is ignored. **Re-run the same deauth
test afterwards**  clients should now stay connected, proving the upgrade closed
the hole. That before/after is the point: use Ereshkigal to justify and verify a
WPA2 → WPA3 migration.

> Only against a network you own or are authorized to test, in your controlled lab.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| **No COM ports** | Install the USB-serial driver; use a data (not charge-only) cable. |
| **"Failed to open COM…"** | Another program holds the port (a serial monitor, another flasher). Close it. |
| **Keeps retrying, then fails** | Do the Download mode sequence while it retries: hold BOOT, tap RESET, release BOOT. |
| **Still failing** | Lower **Speed** to `921600` and flash again. |

## About the firmware format

`Ereshkigal.efw` is the firmware in Ereshkigal's own packaged format. The flasher
prepares it for the board internally you never unpack anything and no extra
tools are involved. Keep the `.exe` and `.efw` together.

---

<div align="center">
<sub>Ereshkigal by <b>Titan Digitalsoft</b> · Flasher 2.0.0 · Authorized testing only</sub>
</div>
