# Safety policy

Status: proposed mandatory constraints for future implementations; no hardware validation yet.

Persistent configuration and device-restriction operations are outside the project scope. Their effects have not been verified on hardware. Do not test, modify or bypass them.

## Mandatory constraints

- Match VID:PID 20A0:41ED and explicitly select the device.
- No automatic initialization or shutdown writes.
- Fail closed: allow exact tuples of direction, request, value, index, length and validated payload, not merely opcode families.
- Prohibit EEPROM (0x1C OUT), flash management (0x0F OUT), flash data (0x10 OUT), firmware updates, bootloader entry, standby brightness and arbitrary packet injection.
- Do not assume an IN request is safe. Initially restrict device tests to documented firmware and serial queries.
- Framebuffer capture is excluded because the original procedure issues flash-family commands before and after reading.
- Check transfer status and actual length, serialize transfers and stop on anomalies.
- No telemetry, network dependency or device-restriction management. Redact device serials in public logs.
- No command fuzzing or persistent writes in initial hardware validation.

See the dated audit for evidence and limitations.
