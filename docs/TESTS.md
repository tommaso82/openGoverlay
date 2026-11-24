# Hardware validation plan

No hardware tests have been performed.

1. Record device revision, USB descriptors, driver binding and baseline display state.
2. Close the original application; avoid concurrent USB access.
3. Independently review the exact firmware and serial query tuples, then run only those queries. Record raw replies, status and lengths; redact serial before publication.
4. After review, separately authorize pixel read, normal brightness and simple graphic primitives.
5. Each visual test must hold its result indefinitely until explicit operator confirmation. Show expected appearance and exact test identifier before sending; record observed results, packets and anomalies. Never advance on a timer.
6. Stop on any unexpected result, short transfer or disconnect. No retries of unknown operations.
7. Do not test EEPROM, flash, bootloader, firmware update, blacklist or framebuffer capture in the initial phase.

Future tests must distinguish static inference, passive capture and physically verified behavior; record firmware revision for every result.
