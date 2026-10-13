---
name: ps1-disc-research
description: Inspect local PlayStation 1 CUE/BIN, ISO and PS-X EXE files, identify and preserve the boot executable, and trace its bytes to original disc sectors. Use for PS1 disc research and preparation for static analysis.
metadata:
  version: "0.3.0"
---

Use the user's local disc or complete executable. Python 3.10+ and its standard
library are required. Resolve `scripts/ps1_inspect.py` relative to this skill
folder, independently of the working directory.

```sh
python3 /path/to/ps1-disc-research/scripts/ps1_inspect.py /local/disc.cue \
  --out /local/evidence/disc.json --boot-out /local/evidence/boot.psx
```

Prefer the original CUE and retain its companions. For ZIP input, inventory and
extract it with the available archive workflow first. Output paths must be new.
Omit them for inspection without writing. Stdout gives boot facts, hashes,
sector mapping and an inventory count; `--out` retains the full inventory, and
`--full` includes it on stdout when needed.

Keep the initial PC and load address distinct. The complete boot copy retains
its 2 KiB header, payload and trailing bytes. Header declarations and static
inspection do not establish executed behavior or a valid engine load.

For deeper analysis, read [playstation-discs.md](references/playstation-discs.md).
It describes supported layouts, budgets, provenance, output requirements and
handoff to REA or another provider advertising PS-X support. Preserve the helper
report alongside later analysis evidence, and compare executable hashes.

Follow the user's research objective. Return evidence paths, observed mappings,
limitations and the next useful analysis step. The helper performs no network
access or target-code execution. Keep private discs, BIOS and extracted bytes
out of public packages and reports.
