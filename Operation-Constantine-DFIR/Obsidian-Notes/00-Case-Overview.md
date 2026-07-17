# Operation Constantine — Case Overview

**Report #:** 20
**Scenario ID:** Operation Constantine — Disk Acquisition (50_55)-18-20
**Analyst:** Salman Mohammed AL Mayasi
**Team:** Blue Team Bootcamp (Golden)
**Date:** July 2026

---

## The Case

| | |
|---|---|
| **Attacker** | Constantine Group |
| **Platform** | MITRE Caldera |
| **Victim host** | DESKTOP-2A1O8LD |
| **Victim user** | anmar |
| **Victim IP** | 192.168.67.129 |
| **C2 server** | 192.168.67.128:8888 |
| **Agent** | `splunkd.exe` (masqueraded as Splunk) |
| **Abilities executed** | 35 |
| **Unique techniques** | 26 |
| **Attack window** | 2026-07-05 07:58:40Z → 08:28:32Z (29m 52s) |

## Attack Summary

A Caldera agent disguised as `splunkd.exe` ran 35 automated abilities in under 30 minutes. It enumerated the system, dumped LSASS credentials, disabled Defender and the firewall, cleared logs, created a hidden `$` account, staged sensitive files, compressed them, and exfiltrated the archive to the C2 server.

## Navigation

- [[01-Evidence-Log]] — evidence and hashes
- [[02-Timeline]] — full chronological timeline
- [[03-Flags]] — CTF flags and answers
- [[04-Techniques]] — MITRE techniques confirmed
- [[05-Lessons]] — lessons learned