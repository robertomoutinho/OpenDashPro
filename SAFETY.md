# Safety and disclaimer

OpenDashPro is **experimental, unofficial software**, provided **as is, with no warranty of any kind**. The authors accept no liability for damage to vehicles, engines, the dash or anything else, or for injury, resulting from its use. Use it at your own risk.

## It can be wrong
- **Decoders are written from public protocol documents, not certified against each ECU.** Some scales and meanings are still unconfirmed on a real car. For example, the FuelTech G-force scale and whether its MAP is relative.
- **Wrong setup gives wrong numbers.** A layout built for a different ECU, the wrong DATA source, a wrong Megasquirt sensor mapping or a wrong unit all produce plausible-looking but wrong values.
- **Gauges can stop updating.** If CAN goes quiet for 1 s, values show `--` and **NO CAN DATA** appears. If the firmware itself hangs, the screen can freeze on the last values. This dash has no usable hardware watchdog.

## Before you rely on it
1. Check every gauge against the ECU's own software (live data) with the engine running: RPM, coolant temperature, oil pressure, AFR/λ, boost.
2. Check every alert actually triggers: lower its threshold on the dash temporarily (Menu → ALERT LEDS).
3. Keep the ECU's protections active: rev limit, overheat and oil-pressure cut, boost cut. **The dash is a display, not a safety system.**
4. Don't adjust the dash while driving.

## It transmits on the CAN bus (Injepro S8000 source only)
Every other source only listens. With **INJEPRO S8000** selected, the dash sends read requests to the ECU (`RI`, and `VFE` if names are read over CAN). The stock dash uses the same requests, and they don't change anything in the ECU. Don't select this source on a bus without an Injepro ECU. Since B00000B9 the dash only sends while it hears traffic on the bus (the S8000 always transmits something), and at the first transmit error (B00000BA: error counter rising, failed send, error passive or bus off) it cancels the queued requests and pauses, 1 s doubling up to 30 s while errors repeat, so a missing ECU or a wiring fault doesn't flood the bus with retries and error frames.

## Hardware
Installing OpenDashPro uses only the dash's USB bootloader, which is never written. The stock firmware can always be re-installed. Opening the case, or flashing with a programmer, is outside this project and can permanently lose the stock bootloader.

This project is not affiliated with, endorsed by or supported by Injepro, AiM, FuelTech or the Megasquirt project. For help with OpenDashPro, don't contact them.
