# PS1 Disc Research

An independently installable agent skill for local PlayStation 1 disc inspection.
Find and preserve the complete boot executable, keep initial PC separate from
load address, and map every extracted byte back to its original disc sector.
Python 3.10+ standard library only.

## Install

```sh
npx skills add Bobtoshi/ps1-disc-research --skill ps1-disc-research
```

The skill works independently. REA is optional for subsequent executable
analysis, and its connected provider must advertise PS-X EXE support.
The proposed [REA loader](https://github.com/morluto/rea/pull/1948) is not proof
that an installed REA release supports it.

## Inspect

Resolve the script inside the installed skill folder:

```sh
python3 skills/ps1-disc-research/scripts/ps1_inspect.py /local/disc.cue \
  --out /local/evidence/disc.json --boot-out /local/evidence/boot.psx
```

Omit output paths to inspect without writing. Stdout is compact; `--out` keeps
the complete inventory and `--full` returns it inline. Outputs require new paths
and a filesystem supporting hard links. Files publish individually.

Supports cooked ISO and Mode1/Mode2 Form1 layouts, one data track with optional
audio, nested SYSTEM.CNF and PSX.EXE fallback. Sources are fully hashed and
rechecked. CUE text, directory processing and executable reads are bounded.
See [the skill](skills/ps1-disc-research/SKILL.md) for usage and limitations.
No games, BIOS, SDK, saves or extracted commercial data are distributed.

## Verify

```sh
python3 -B -m unittest discover -s tests -v
```

The tests use synthetic source-owned fixtures and verify CLI reports, complete
boot-byte preservation, source mutation, size/growth limits, explicit ISO file
versions, numeric token bounds, aggregate directory reads and provenance.
They do not establish emulation or native-analysis provider compatibility.

## Origin

Developed from the PS1 research prototype and the static inspector reviewed in
[REA PR #2386](https://github.com/morluto/rea/pull/2386), which was closed in favor
of an individual skill. MIT licensed; see [NOTICE](NOTICE) for attribution.
