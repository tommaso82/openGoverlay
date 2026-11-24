# Research log

## 2026-11-24 — Initial static audit

Analyzed the owner-provided GOverlay v1.69 portable distribution using a local PE/CLI metadata and CIL reader. No proprietary executable was run and no USB packets were sent. Identified the LCDsysinfo2 class, vendor control transfers, graphics primitives and persistent-write hazards. Verified archive and binary SHA-256 values against the dated audit.

Outstanding: complete byte layouts for text, icons, progress bars, lines and shapes; firmware version gates and color conversions; static native updater/resource analysis; passive capture and controlled hardware validation.

Public background references (not evidence that older drivers support the 3.5-inch model):
- https://www.goverlay.com/content/lcdsysinfo2
- https://github.com/dangardner/pylcdsysinfo
- https://github.com/kdar/golcdsysinfo
- https://github.com/samccone/lcdsysinfo

Research by tommaso82 in collaboration with ChatGPT (OpenAI).
