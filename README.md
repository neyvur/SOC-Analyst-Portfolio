# SOC Analyst Portfolio

> A hands-on learning portfolio focused on Security Operations, security monitoring, detection engineering, incident investigation, and network analysis.

**Status:** In progress  
**Focus:** Blue Team · SOC Analyst L1 · Detection & Incident Response

---

## About

This repository documents practical cybersecurity labs and investigations completed in controlled, authorized environments. Each project is intended to show the full analytical workflow: collecting evidence, validating suspicious activity, documenting findings, and recommending appropriate response actions.

This is a learning portfolio, not a claim of professional SOC employment or production incident-response experience.

## Technical areas

- Security monitoring and SIEM
- Linux authentication and system logs
- Windows event telemetry and Sysmon
- Incident triage and investigation
- Detection logic and false-positive review
- Network traffic and DNS analysis
- IOC enrichment and MITRE ATT&CK mapping

## Tools

Tools will be added here only after they have been used and documented in a project.

| Tool / technology | Intended use | Status |
|---|---|---|
| Docker | Reproducible lab environments | Planned |
| Wazuh | SIEM and endpoint monitoring | Planned |
| Linux | Authentication and system-log analysis | Learning |
| Python | Log parsing and small automation scripts | Learning |
| Wireshark | Packet and network traffic analysis | Planned |
| Sigma | Portable detection rules | Planned |
| Sysmon | Windows event telemetry | Planned |
| MITRE ATT&CK | Tactic and technique mapping | Reference |

## Projects

| Project | What it demonstrates | Status |
|---|---|---|
| [01 — SOC Monitoring Lab](01-soc-monitoring-lab/) | Lab setup, log collection, alert review | Planned |
| [02 — Incident Response](02-incident-response/) | Evidence-based investigation and incident reports | Planned |
| [03 — Detection Engineering](03-detection-engineering/) | Detection rules, validation, false-positive analysis | Planned |
| [04 — Network Analysis](04-network-analysis/) | PCAP, DNS, and network investigation | Planned |
| [05 — Windows Forensics](05-windows-forensics/) | Windows event and Sysmon analysis | Planned |
| [06 — Threat Intelligence](06-threat-intelligence/) | IOC enrichment and threat context | Planned |

> Update each status only when the work exists and the evidence has been checked into the repository.

## Investigation workflow

For each case, I aim to follow this workflow:

1. **Scope** — define the system, time range, and question being investigated.
2. **Collect** — preserve relevant logs, events, or packet-capture evidence.
3. **Triage** — identify suspicious indicators and prioritize the alert.
4. **Investigate** — correlate timestamps, users, processes, IPs, and related events.
5. **Assess** — distinguish confirmed malicious activity from suspicious or benign activity.
6. **Map** — map relevant behavior to MITRE ATT&CK when appropriate.
7. **Respond** — recommend containment, remediation, and recovery actions.
8. **Document** — record evidence, limitations, conclusion, and lessons learned.

## Repository structure

```text
SOC-Analyst-Portfolio/
├── 01-soc-monitoring-lab/
│   ├── wazuh/
│   ├── linux-endpoint/
│   └── evidence/
├── 02-incident-response/
│   ├── ssh-brute-force/
│   ├── phishing-investigation/
│   └── suspicious-powershell/
├── 03-detection-engineering/
│   ├── sigma-rules/
│   ├── wazuh-rules/
│   └── test-results/
├── 04-network-analysis/
│   ├── pcap-analysis/
│   └── dns-investigation/
├── 05-windows-forensics/
├── 06-threat-intelligence/
└── docs/
```

## Evidence and reporting standards

Each completed investigation should include, where applicable:

- A concise README describing the objective and lab setup
- Sanitized sample logs or a reference to the original public dataset
- Screenshots that show the relevant tool output
- Detection logic and test results
- An incident report with timeline, findings, severity rationale, and recommendations
- Limitations, assumptions, and false-positive considerations

Severity is assigned based on evidence and context; an alert alone does not prove compromise.

## Safety and responsible use

- All testing is performed on systems I own, administer, or have explicit permission to assess.
- Attack simulations use controlled lab environments and non-production accounts.
- Secrets, passwords, access tokens, personal data, and sensitive logs are never committed.
- Public sample data is attributed to its source and license where applicable.
- Potentially harmful samples are not executed on the host machine.

## About the author

Cybersecurity student building practical skills in Blue Team operations, security monitoring, and incident investigation.

**Current goal:** prepare for an entry-level SOC Analyst role by documenting repeatable, evidence-based investigations.

---

*This repository is actively maintained. Project status and tool proficiency are updated as work is completed.*
