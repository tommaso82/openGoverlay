# Safety policy

Status: proposed mandatory constraints for future implementations; no hardware validation yet.

The original v1.69 host application contains an online blacklist path: Form1::WebBrowser_Check_DocumentCompleted (MethodDef 2205, IL 0x0026–0x004B) calls LCDsysinfo2::BlockUnit (2720) on a matching response. BlockUnit calls WriteEprom (2722) with address 15 and value 137. The vendor updater uses HTTP. Firmware enforcement, reversibility and the original EEPROM value are unknown. Do not deliberately set or clear this marker. The original GetLockedStatus (2721) requests zero bytes despite allocating a 12-byte buffer and then examines byte 7; it is not a reliable diagnostic.

## Mandatory constraints

- Match VID:PID 20A0:41ED and explicitly select the device.
- No automatic initialization or shutdown writes.
- Fail closed: allow exact tuples of direction, request, value, index, length and validated payload, not merely opcode families.
- Prohibit EEPROM (0x1C OUT), flash management (0x0F OUT), flash data (0x10 OUT), firmware updates, bootloader entry, standby brightness and arbitrary packet injection.
- Do not assume an IN request is safe. Initially restrict device tests to documented firmware and serial queries.
- Framebuffer capture is excluded because the original procedure issues flash-family commands before and after reading.
- Check transfer status and actual length, serialize transfers and stop on anomalies.
- No telemetry, network dependency or remote blacklist. Redact device serials in public logs.
- No command fuzzing or persistent writes in initial hardware validation.

See the dated audit for evidence and limitations.
