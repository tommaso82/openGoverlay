# USB protocol reference

Research draft, 2026-11-24. Static host-side observations only, not a validated firmware specification.

Target: LCDSysInfo GOverlay 3.5-inch, VID:PID 20A0:41ED. Display 480 × 320, RGB565 in host transfers. Vendor-specific device control transfers: OUT 0x40, IN 0xC0. Setup fields are little-endian on the bus; many graphic payload fields are big-endian. Original LibUsbDotNet calls often set setup Length to zero and pass the actual length separately. Preserve the actual transfer length in any new API.

| Direction | Request (hex) | Observed purpose |
|---|---|---|
| IN | 0C | Identification, status, screen/flash reads |
| IN | 88 | Pixel read |
| OUT | 0D | Normal brightness |
| OUT | 0E | Blink |
| OUT | 0F | Flash management/mode; prohibited |
| OUT | 10 | Flash data; prohibited |
| OUT | 19 | Built-in font text |
| OUT | 1A | Clear regions |
| OUT | 1C | EEPROM; prohibited |
| OUT | 1D | Icon |
| OUT | 1E | Background |
| OUT | 21 | Progress bar |
| OUT | 22 | Connected lines |
| OUT | 86 | Independent lines |
| OUT | BD | Font spacing |
| OUT | BE | Custom font text |
| OUT | BF | Graphics primitives |
| OUT | C0 | Multiple icons |
| OUT | C1 | Alternative icon |

This is an observed host-side catalog, not an exhaustive firmware opcode list.

| Type hex | Request hex | Value | Index | Actual data length | Evidence |
|---|---|---|---|---|---|
| C0 | 0C | 0 | 1 | 8 IN | init 2718 IL 0x0210–0x0241 |
| C0 | 0C | 0 | 5 | 8 IN | init 2718 IL 0x01BB–0x01EC |
| C0 | 88 | X | Y | 2 IN | getpixel 2756 IL 0x0044–0x006B |
| 40 | 0D | B | B | 0 | brightness 2726 IL 0x0068–0x007E |
| 40 | 1E | color | 0 | 0 | SetBackground 2742 IL 0x003E–0x0071 |
| 40 | 1A | mask | color | 0 | ClearLines 2744 IL 0x00FD–0x0113 |

Parameters and lengths in decimal unless specified. Firmware is response byte 1 (zero-based); serial is eight raw bytes. Pixel response is big-endian RGB565. Bounds X 0–479, Y 0–319; brightness 0–255. Clear mask is six bits, 63 selects all. Region geometry unverified.

Draw_Pixels (2754): BF, index 4, value 6 × element count; payload Y,X,color, each 16-bit big-endian. Rectangle payload Y1,X1,Y2,X2,color; rounded variant adds radius. Exact variants pending. Built-in font IDs regular=0, regular_small=1; ASCII encoding and special transparent value 12345. Custom font uses BE. Connected lines use 22 and value point count minus one; independent lines use 86. Do not assume uniform coordinate order.

See SAFETY.md before any device access. No request in this reference is hardware validated.
