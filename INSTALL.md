# Installing OpenDashPro

**Read SAFETY.md first.** This is experimental software for a display in a vehicle.

## What's in the download
| File | What it is |
|---|---|
| `OpenDashPro Studio-<version>-arm64.dmg` | Studio for Macs with Apple silicon (M1 and later) |
| `OpenDashPro Studio-<version>.dmg` | Studio for Intel Macs |
| `OpenDashPro Studio Setup <version>.exe` | Studio for Windows (64-bit) |
| `OpenDashPro Studio-<version>.AppImage` | Studio for Linux (64-bit x86) |
| `opendashpro-<version>.hex` | The dash firmware on its own. Studio already includes it. |
| `SHA256SUMS.txt` | Checksums for checking the download |

## 1. Install Studio
- **Mac:** open the .dmg and drag OpenDashPro Studio to Applications. The app isn't notarized by Apple, so the first launch is blocked. Right-click the app → **Open** → **Open**. On recent macOS, go to System Settings → Privacy & Security and click **Open Anyway**.
- **Windows:** run the installer. SmartScreen will warn because the app isn't signed. Click **More info** → **Run anyway**. No USB driver is needed (the dash and its bootloader are standard USB HID devices).
- **Linux:** make the AppImage executable and run it (`chmod +x "OpenDashPro Studio-<version>.AppImage"`). Ordinary users can't open USB HID devices until a udev rule allows it. Once, as root:
  ```
  echo 'KERNEL=="hidraw*", ATTRS{idVendor}=="04d8", ATTRS{idProduct}=="003c|00da|00db", MODE="0666"' | sudo tee /etc/udev/rules.d/99-opendashpro.rules
  sudo udevadm control --reload-rules && sudo udevadm trigger
  ```
  (`003c` is the dash's USB bootloader, which Studio flashes through; `00da` the stock firmware; `00db` the running OpenDashPro.) Then replug the dash.

## 2. Put OpenDashPro on the dash (first time)
1. Connect the dash to the computer with USB.
2. In Studio, click **Flash DashPro (.hex)…** → **Flash**.
3. When asked, **unplug and replug the dash's USB**. The dash restarts into its USB bootloader, and Studio flashes it. The screen flickers or shows garbage while this happens. That's normal. **Don't unplug it until Studio says it's done.**
4. The dash restarts with OpenDashPro and the OpenDashPro splash.

## 3. Set it up
On the dash: tap the screen, then the top centre, to open the **Menu**.
1. **CALIBRATE TOUCH** (touch and hold each of the 4 crosses).
2. **DATA:** pick your ECU's protocol (AiM CAN, FTCAN 2.0, Megasquirt or Injepro S8000), and turn on the matching dash/CAN output in your ECU's software. If **NO CAN DATA** shows, use **CAN MONITOR** to check the wiring and bus speed.
3. Brightness: tap the screen and use the slider at the bottom.

## 4. Your own layout
In Studio, pick your **ECU** in the top bar and design the layout. Then on the dash, open Menu → **USB UPDATE MODE** (or replug USB) and click **Upload (persist) ⬆**. 

## Going back to the stock firmware
OpenDashPro never touches the dash's bootloader. Re-install the stock firmware with the vendor's own updater, the same way you'd update it normally.

## Licence
Free for personal, noncommercial use. No redistribution and no modification. See LICENSE.
