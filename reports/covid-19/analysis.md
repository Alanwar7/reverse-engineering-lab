# Static Malware Analysis: Baby Ransom

## 1. Executive Summary

This report documents the static analysis of a Linux ELF executable identified as a ransomware-like sample named `covid-19`, obtained from crackmes.one.

The sample contains a ransom demand requesting 0.2 Bitcoin in exchange for access to files. Analysis in Ghidra identified directory traversal, filename processing, file input/output, file removal, and an apparent XOR-based file transformation.

The analysis focused on understanding the program's structure and behavior without executing the sample.

## 2. Sample Information

| Property          | Value           |
| ----------------- | --------------- |
| Sample name       | covid-19        |
| File format       | ELF             |
| Architecture      | 64-bit          |
| Source            | crackmes.one    |
| SHA-256           | To be recorded  |
| Analysis method   | Static analysis |
| Primary tool      | Ghidra          |
| Dynamic execution | Not performed   |

## 3. Analysis Environment

The sample was examined in a Kali Linux virtual machine using Ghidra.

The analysis involved examining decompiled pseudocode, identifying functions and cross-references, and tracing data flow between directory handling, file operations, and the suspected encryption routine.

The sample was not intentionally executed during this analysis. The virtual machine was prepared for isolated analysis.

## 4. Behavioral Analysis

### 4.1 Directory Traversal

The function renamed as `BigBoy` uses `opendir()` and `readdir()` to open and enumerate a directory.

The code compares directory-entry names against a string using functions such as `strcmp()` and `strstr()`. This suggests that the program selects files based on filename-related conditions.

The exact directory scope and complete selection criteria require further verification.

### 4.2 File Processing

The identified function uses file operations including `fopen()`, `fgetc()`, `fputc()`, and `fclose()`.

The code appears to read data from a file, transform data conditionally, and write output to another stream. It also calls `remove()` on a directory-entry filename.

The precise relationship between the input file, output file, and removal operation should be verified by tracing the paths and arguments.

### 4.3 Suspected Encryption Routine

The file-processing loop contains an XOR operation involving a byte read from the input stream and a value derived from a pseudorandom number.

The program calls `srand(0xdeadbeef)` before calling `rand()`. The fixed seed suggests that the pseudorandom sequence is reproducible under the same C library implementation.

This raises concerns about the strength of the transformation. However, the full algorithm, key handling, and behavior across different files and executions have not been conclusively established.

### 4.4 Filename Processing

The function renamed as `slashes` manipulates strings using `strcat()`, `strstr()`, and `strncpy()`. The string `.corona` appears in this function.

The exact purpose of this routine has not yet been established.

### 4.5 Ransom Demand

The executable contains a ransom message requesting 0.2 Bitcoin to regain access to files.

This message, combined with the file-processing logic, supports classifying the sample as ransomware-like. The complete runtime behavior has not been verified.

## 5. Notable Strings and Artifacts

The following strings were observed during analysis:

- `Transfer 0.2 Bitcoin to access your files` — ransom demand; record the exact original wording from the sample.
- `.corona` — appears in filename-processing logic.
- Other unusual strings should be documented only when their relevance can be established.

The sample's SHA-256 hash should be recorded to identify the exact analyzed file.

## 6. Limitations and Unresolved Questions

The following questions remain open:

- What exact files and directories does the program target?
- What are the precise input and output paths used during file processing?
- Does the XOR transformation execute for every byte and file?
- How does the fixed-seed pseudorandom sequence influence the transformation?
- What role does the `littleboy` function and its `xstat` call play?
- What is the exact behavior of the ransom-note routine?
- Does the program implement any persistence, process manipulation, or additional destructive behavior?

These questions require further static/ dynamic analysis before definitive conclusions can be made.

## 7. Conclusion

Static analysis identified directory enumeration, filename processing, file reading and writing, file removal, an apparent XOR-based transformation, and a ransom demand.

The combination of these behaviors is consistent with a ransomware-like program. However, the complete encryption scheme, file-selection scope, and runtime effects remain unverified.

The analysis demonstrates how Ghidra can be used to reconstruct program behavior through function inspection, cross-references, and data-flow analysis without executing a suspicious binary.
