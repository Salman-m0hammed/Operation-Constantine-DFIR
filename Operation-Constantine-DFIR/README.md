# Operation Constantine — DFIR Investigation

Forensic investigation of a Windows 10 workstation compromised by an automated adversary emulation platform (MITRE Caldera).

**Report #20** | Blue Team Bootcamp (Golden) | July 2026

---

## Overview

| | |
|---|---|
| **Attacker** | Constantine Group |
| **Platform** | MITRE Caldera |
| **Agent** | `splunkd.exe` (masqueraded) |
| **C2** | 192.168.67.128:8888 |
| **Duration** | 29 min 52 sec |
| **Abilities** | 35 |
| **Techniques** | 26 unique MITRE ATT&CK |

## Key Findings

- **T1003.001** — Sysmon Event ID 10: `splunkd.exe` accessed `lsass.exe` with `GrantedAccess 0x1FFFFF`
- **T1564** — Hidden local account `$` created at 08:20:22Z, invisible to `net user`
- **T1041** — `staged.zip` (155,287 bytes) exfiltrated via `POST /file/upload`
- **T1071** — Caldera Sandcat beacon (`Go-http-client/1.1`) to port 8888

## Techniques Expected but Not Found

The task documentation listed three techniques that the evidence does not support:

| Technique | Verification |
|---|---|
| T1547.001 (Run Key) | HKLM Run, HKCU Run, and Winlogon all examined — clean |
| T1134 (Token Manipulation) | Agent deployed already at `privilege: Elevated` |
| T1016 (Network Config Discovery) | Not executed; T1135 and T1018 used instead |

## Contents

- [`Report/`](Report/) — Full incident report
- [`Obsidian-Notes/`](Obsidian-Notes/) — Case notes (Obsidian vault)
- [`Detection-Rules/`](Detection-Rules/) — Sigma rule for T1003.001
- [`Knowledge-Graph/`](Knowledge-Graph/) — Attack chain diagram (draw.io)
- [`Screenshots/`](Screenshots/) — Evidence screenshots

## Tools

FTK Imager · Registry Explorer (Eric Zimmerman) · Event Viewer · Wireshark · CyberChef · Sigma

## Author

**Salman Mohammed AL Mayasi** — Blue Team / DFIR Analyst