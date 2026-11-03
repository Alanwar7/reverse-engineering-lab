# Reverse Engineering Report Template

Copy this file to `reports/<sample-name>/analysis.md` for each new project.

## 1. Overview

- **Sample / challenge:**
- **Category:** Crackme / malware sample / CTF / other
- **Source:**
- **Date analyzed:**
- **Analysis type:** Static / dynamic / both
- **Status:** In progress / completed / partial

### Summary

Briefly describe what the program appears to do and the main findings. Clearly qualify anything not confirmed.

## 2. Sample Identification

| Property | Value |
|---|---|
| Filename | |
| SHA-256 | |
| File format | |
| Architecture | |
| Endianness | |
| Entry point | |
| Compiler / build information (if known) | |

Do not include the binary itself unless there is a specific, safe, and permitted reason.

## 3. Lab Environment

- **Host OS:**
- **Guest OS / VM:**
- **Isolation controls:**
- **Tools and versions:**
- **Snapshot / restore point:**

State whether the sample was executed. Do not imply dynamic analysis if only static analysis was performed.

## 4. Initial Reconnaissance

Record commands and observations.

| Check | Command / method | Observation |
|---|---|---|
| File identification | `file <sample>` | |
| ELF / PE metadata | `readelf -h` / relevant tool | |
| Hash | `sha256sum <sample>` | |
| Strings | `strings -a <sample>` | |
| Imports / symbols | | |

## 5. Program Structure

Describe the entry point, important functions, and how they relate.

| Function / address | Observed responsibility | Evidence / confidence |
|---|---|---|
| | | |

Include a simple call-flow diagram if it helps.

## 6. Detailed Technical Analysis

### 6.1 Input and arguments

- What inputs does the program accept?
- Where are they read?
- What validation occurs?

### 6.2 Important algorithms and logic

Explain loops, conditions, transformations, comparisons, and data structures. Include short pseudocode excerpts only where useful.

### 6.3 File, network, and process behavior

Document relevant operations and their arguments. Distinguish observed code paths from behavior confirmed at runtime.

### 6.4 Cryptography / obfuscation (if applicable)

- Algorithm or transformation:
- Key / seed / nonce handling:
- Data flow:
- What is confirmed:
- What remains uncertain:

Do not label a transformation secure encryption without sufficient evidence.

## 7. Indicators and Artifacts

List relevant strings, filenames, hashes, paths, domains, or other artifacts. Explain why each matters. Avoid including secrets or personal data.

## 8. Findings

| ID | Finding | Evidence | Confidence |
|---|---|---|---|
| F-01 | | | High / Medium / Low |

Use confidence carefully:
- **High:** directly supported by clear code or repeatable observation.
- **Medium:** supported by evidence, but interpretation has uncertainty.
- **Low:** plausible hypothesis requiring more investigation.

## 9. Limitations and Unresolved Questions

- 
- 
- 

State what you did not test and why.

## 10. Conclusion

Summarize what you established, the techniques used, and the most important remaining uncertainty.

## 11. References

- Documentation:
- Tools:
- Challenge / sample source:

## Appendix: Screenshots

Store screenshots in `screenshots/` and embed them with relative paths, for example:

```markdown
![Function showing file enumeration](screenshots/file-enumeration.png)
```

Add a caption explaining what the screenshot demonstrates. Crop screenshots to the relevant code and remove usernames, local paths, tokens, and unrelated desktop content where appropriate.
