# Incident #001 — Linux File Integrity Modification

## 1. Overview

| Field | Value |
|---|---|
| Incident ID | INC-001 |
| Date | 2026-11-21 |
| Host | linux-endpoint-01 |
| Operating System | Debian 12 |
| SIEM | Wazuh 4.14.10 |
| Detection Type | File Integrity Monitoring (FIM) |
| Wazuh Rule ID | 550 |
| Severity | Level 7 |
| MITRE ATT&CK | T1565.001 — Stored Data Manipulation |
| Classification | Benign — Authorized Lab Simulation |

## 2. Objective

Validate Wazuh File Integrity Monitoring by creating and modifying a test file on a monitored Linux endpoint.

The objective was to verify real-time file change detection and analyze the resulting security event.

## 3. Environment

- Wazuh Manager: wazuh.manager
- Wazuh Agent: linux-endpoint-01
- Agent ID: 001
- Agent IP: 172.20.0.5
- Monitored directory: /root/fim-lab
- Monitoring mode: realtime

## 4. Detection Timeline

| Timestamp | Event | Description |
|---|---|---|
| 10:12:16.736 | File added | Test file created |
| 10:12:55.842 | File modified | File content modified |

Target file:

`/root/fim-lab/test-file.txt`

Wazuh detected both events.

## 5. Alert Analysis

### Wazuh Rule

- Rule ID: 550
- Description: Integrity checksum changed.
- Severity: 7
- Decoder: syscheck_integrity_changed
- Event: modified
- Detection mode: realtime

### Changed Attributes

- File size
- Modification time (mtime)
- MD5 checksum
- SHA1 checksum
- SHA256 checksum

### File Size

- Before: 28 bytes
- After: 95 bytes

### MD5

Before:
`df2abd98d03159b4237638b19dca3eb9`

After:
`f138a8d2cb07ff85f321cdf853d216c3`

### SHA1

Before:
`cfaa2cdc83912faf3e745bbf32c3ca14dd67ef79`

After:
`88cab30b2c6664715c52a8738a259894f6764356`

### SHA256

Before:
`83784f5070ae3b4622cc73da50fa4094335baa52fd3a51f3aeeaf5f145c096cc`

After:
`85f8975d5a703e21c5ded10fc08a198e9f1e7935434b6f9cdb1e34aeb3d15f15`

## 6. MITRE ATT&CK Mapping

- Tactic: Impact
- Technique: T1565.001
- Name: Stored Data Manipulation

This mapping indicates a potential relationship between file modification and data manipulation techniques. It does not independently establish malicious activity.

## 7. Investigation

The alert confirmed that Wazuh detected a change to the monitored file.

The SHA256 checksum changed, confirming that the file content was different after modification.

The file was owned by root. However, file ownership alone does not identify the process or user responsible for the modification.

The activity was intentionally generated as part of this laboratory exercise.

## 8. Analyst Verdict

Classification: BENIGN — AUTHORIZED TEST

Reason:
The file creation and modification were performed intentionally to validate FIM functionality.

No evidence of an actual compromise was established.

## 9. Detection Limitations

FIM identifies file changes but does not, by itself, establish:

- Which process performed the modification.
- Which user initiated the action.
- Whether the modification was malicious or legitimate.

Additional endpoint telemetry and event correlation would be required for deeper attribution.

## 10. Outcome

- [x] Linux endpoint connected to Wazuh Manager.
- [x] FIM enabled.
- [x] Real-time monitoring configured.
- [x] File creation detected.
- [x] File modification detected.
- [x] Checksum changes analyzed.
- [x] MITRE ATT&CK mapping reviewed.
- [x] Incident classification documented.

**Result:** Successful validation of Wazuh FIM detection on a Linux endpoint.

## 11. Visual Evidence

### FIM Event Detection

The Wazuh Dashboard detected two file integrity events: file creation and modification.

![FIM Event Detection](Screenshot%202026-11-21%20at%2010.23.45.png)

### Alert Details

Detailed analysis of the file modification event, including changed attributes and checksums.

![Wazuh Alert Details](Screenshot%202026-11-21%20at%2010.29.06.png)

### Additional Dashboard Evidence

![Additional Dashboard Evidence](Screenshot%202026-11-21%20at%2010.29.24.png)
