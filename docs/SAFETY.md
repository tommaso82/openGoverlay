# Safety policy

Proposed mandatory requirements for the independent implementation. No hardware validation yet.

- Identify and explicitly select the supported display.
- No automatic persistent writes at connection or disconnection.
- Allow only reviewed operations with validated parameters. Reject unknown commands.
- Exclude firmware updates, bootloader entry, persistent configuration changes, protection-related operations and arbitrary packet injection from the initial implementation.
- Do not assume a read operation is harmless; review every request.
- Check transfer results and lengths, serialize operations and stop on anomalies.
- No telemetry or vendor-service dependencies.
- Redact device identifiers and personal data from public logs.
- No command fuzzing or destructive tests.

See [INTEROPERABILITY.md](INTEROPERABILITY.md) and [TESTS.md](TESTS.md).
