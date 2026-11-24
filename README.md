# OpenGOverlay

Independent USB protocol research and planned lightweight open-source driver for the LCDSysInfo GOverlay 3.5-inch display (480 × 320, USB VID:PID `20A0:41ED`).

**Status: research only. No working driver or hardware validation yet.** Findings from the original GOverlay v1.69 host software are not proof of firmware behavior.

## Goals

- Standalone, lightweight Windows and Linux support.
- Local operation without the original GOverlay application, telemetry, remote blacklist or vendor servers.
- Documented USB commands, reproducible findings and controlled hardware tests.
- Native display primitives and efficient incremental updates.
- No proprietary binaries, extracted artwork or decompiled source distributed here.

## Documentation

- [Protocol reference](docs/PROTOCOL.md)
- [Safety rules](docs/SAFETY.md)
- [Original static audit (Italian)](docs/AUDIT-2026-11-24.md)
- [Hardware validation plan](docs/TESTS.md)
- [Research log](docs/RESEARCH.md)

## Safety first

The original application contains persistent EEPROM and flash operations, including a remotely triggered blacklist marker. Their actual firmware-side effects are not yet established. OpenGOverlay will use a fail-closed allowlist of exact, validated requests; no automatic persistent writes, firmware updates, raw opcode scanning or remote control.

Do not use this research as an executable command recipe. No hardware commands have been tested.

## Credits

Project owner and hardware testing: [tommaso82](https://github.com/tommaso82).

Protocol research and documentation in collaboration with [ChatGPT (OpenAI)](https://chatgpt.com/). AI-assisted findings require human review and hardware validation.

This is an independent project, not affiliated with Coldtears Electronics or the GOverlay developer.
