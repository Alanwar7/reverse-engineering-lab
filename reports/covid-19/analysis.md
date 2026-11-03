# covid-19 — Static Malware Analysis

## 1. Overview

- **Category:** Ransomware-like ELF sample
- **Source:** crackmes.one
- **Analysis type:** Static analysis
- **Status:** Initial static analysis completed

### Summary

The sample contains a ransom demand requesting 0.2 Bitcoin to regain access to files. Static analysis identified directory enumeration, filename processing, file input/output, file removal, and an apparent XOR-based byte transformation. The complete runtime behavior and cryptographic properties were not verified.

## 2. Sample Identification

| Property | Value |
|---|---|
| Sample name | covid-19 |
| File format | ELF |
| Architecture | 64-bit |
| SHA-256 | To be recorded |
| Source | crackmes.one |
| Dynamic execution | Not performed |

## 3. Analysis Environment

The sample was examined in Kali Linux using Ghidra. Analysis focused on decompiled pseudocode, function references, strings, and data flow. The sample was not intentionally executed during this analysis.

## 4. Behavioral Analysis

### 4.1 Directory traversal — `BigBoy`

The function uses `opendir()` and `readdir()` to enumerate directory entries. It compares entry names using functions including `strcmp()` and `strstr()`, suggesting that files are selected according to filename-related conditions. The exact directory scope and selection criteria require further verification.

### 4.2 File processing

The code uses `fopen()`, `fgetc()`, `fputc()`, and `fclose()` to read and write file data. It also calls `remove()` on a directory-entry filename. The exact relationship between the input path, output path, and removed file should be verified by tracing the arguments and working directory.

### 4.3 Suspected XOR transformation

The file-processing loop contains an XOR operation involving a byte read from an input stream and a value derived from a pseudorandom number. The code calls `srand(0xdeadbeef)` before `rand()`. A fixed seed makes the pseudorandom sequence reproducible for the same C library implementation.

This supports the presence of an XOR-based transformation, but the complete algorithm, key handling, and behavior across files and executions were not conclusively established.

### 4.4 Filename processing — `slashes`

The function uses string operations including `strcat()`, `strstr()`, and `strncpy()`. The string `corona` appears in this logic. Its exact purpose has not yet been established.

### 4.5 File metadata — `littleboy`

The function calls `xstat`. This is associated with retrieving file metadata on some Linux/glibc interfaces, but the exact role in this sample remains to be confirmed by inspecting the call arguments, return value, and subsequent branches.

### 4.6 Ransom demand

The binary contains a message requesting 0.2 Bitcoin to regain access to files. Combined with the file-processing logic, this supports classifying the sample as ransomware-like. Runtime behavior was not verified.

## 5. Notable Strings and Artifacts

- Ransom demand requesting 0.2 Bitcoin — record the exact original wording.
- `corona` — appears in filename-processing logic.

## 6. Limitations and Unresolved Questions

- What exact files and directories are targeted?
- What are the exact input, output, and removal paths?
- Does the XOR transformation execute for every byte and file?
- How does the fixed-seed pseudorandom sequence influence the transformation?
- What role does `littleboy` and its `xstat` call play?
- What is the exact behavior of the ransom-note routine?
- Are there additional behaviors not identified through static analysis?

## 7. Conclusion

Static analysis identified directory enumeration, filename processing, file reading and writing, file removal, an apparent XOR-based transformation, and a ransom demand. The observed behavior is consistent with a ransomware-like program. The complete encryption scheme, file-selection scope, and runtime effects remain unverified.

## Appendix: Screenshots

Add cropped, relevant Ghidra screenshots to this folder. Embed them here with relative paths and captions. Do not include the malware binary in the repository.
