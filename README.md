# Reverse Engineering Lab

A collection of hands-on reverse engineering and malware-analysis exercises. Each report documents the investigation process, evidence, conclusions, and unresolved questions.

## Objectives

- Build practical skills in static and dynamic binary analysis.
- Understand executable structure, assembly, control flow, and data flow.
- Analyze crackmes and suspicious binaries in a controlled lab.
- Document findings clearly and reproducibly.

## Tools

Tools used across projects may include:

- Ghidra — disassembly, decompilation, function and cross-reference analysis
- GDB — runtime debugging and memory inspection
- Linux command-line utilities — `file`, `readelf`, `strings`, `objdump`, `sha256sum`

Only list tools in an individual report if they were actually used for that analysis.

## Repository structure

```text
reverse-engineering-lab/
├── README.md
├── REPORT_TEMPLATE.md
├── .gitignore
└── reports/
    ├── templates/
    │   └── analysis-template.md
    └── covid-19/
        ├── analysis.md
        └── screenshots/
```

Create one folder per sample or challenge under `reports/`. Give each folder an informative, consistent name.

## Reports

| Project | Format / architecture | Focus | Status |
|---|---|---|---|
| [covid-19](reports/covid-19/analysis.md) | 64-bit ELF | Static analysis of ransomware-like behavior | Initial static analysis |

## Adding a new analysis

1. Create a folder: `reports/<sample-name>/`.
2. Copy `reports/templates/analysis-template.md` into it as `analysis.md`.
3. Add relevant, safely redacted screenshots to `screenshots/`.
4. Record the sample's SHA-256 hash and analysis environment.
5. Separate observed facts from hypotheses and unverified behavior.
6. Update the Reports table above.

## Safety and responsible handling

- Do not commit malware binaries, payloads, stolen data, credentials, or live ransom notes containing personal information.
- Publish hashes, source references, pseudocode excerpts, and screenshots only when safe and permitted.
- Do not run malware on a host system or a VM containing personal files.
- A VM snapshot is a recovery aid, not a security boundary.
- Do not publish instructions or artifacts that enable harm. Keep analysis focused on understanding and defensive learning.

## Disclaimer

This repository is for educational and defensive security research. Analysis findings are limited to the evidence documented in each report.
