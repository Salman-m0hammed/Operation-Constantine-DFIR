# Timeline of Events

All times UTC. PCAP is local time — offset noted below.

## Pre-Operation

| Time | Activity | MITRE | Source |
|---|---|---|---|
| 06:13:27 | Agent `splunkd.exe` first check-in (paw: qionqz) | T1071 | Operation report |
| 06:38:48 | Agent `anmar_hacking.exe` deployed (paw: qktity) | T1071 | Operation report |
| 07:28:50 | `splunkd.exe` accesses `lsass.exe` — GrantedAccess `0x1FFFFF` | T1003.001 | Sysmon Event ID 10 |

## Phase 1 — Discovery (07:58 – 08:07)

| Time | Activity | MITRE |
|---|---|---|
| 07:58:40 | Identify active user | T1033 |
| 07:59:25 | Identify local users (`Get-WmiObject Win32_UserAccount`) | T1087.001 |
| 08:00:35 | Find user processes | T1057 |
| 08:01:17 | View admin shares | T1135 |
| 08:02:10 | Discover domain controller | T1018 |
| 08:02:58 | Discover antivirus programs | T1518.001 |
| 08:04:29 | Permission Groups Discovery | T1069.001 |
| 08:04:42 | Identify Firewalls | T1518.001 |
| 08:05:44 | Find files | T1005 |
| 08:06:28 | Find files | T1005 |
| 08:07:13 | Find files | T1005 |

## Phase 2 — Defense Evasion & Stealth (08:07 – 08:24)

| Time | Activity | MITRE |
|---|---|---|
| 08:07:49 | Create staging directory `C:\Windows\system32\staged` | T1074.001 |
| 08:08:37 | Avoid logs | T1070.003 |
| 08:09:44 | Prevent PowerShell history logging | T1070.003 |
| 08:10:47 | **Disable Windows Defender** | T1562.001 |
| 08:11:40 | Grant full folder access to Everyone | T1222.001 |
| 08:12:41 | Move PowerShell & triage | T1059.001 |
| 08:13:32 | **Clear logs** | T1070.001 |
| 08:14:19 | **Disable Defender Firewall** | T1686 |
| 08:15:00 | Create hidden file with `attrib` | T1564.001 |
| 08:15:58 | Change ExecutionPolicy to Bypass | T1112 |
| 08:16:52 | File extension masquerading | T1036.007 |
| 08:17:55 | Hidden window | T1564.003 |
| 08:18:43 | Non-Windows exe masquerading as Windows exe | T1036.003 |
| 08:19:42 | Indicator removal using FSUtil | T1070 |
| 08:20:22 | **Create hidden user `$`** (`net user $ ATOMIC123! /add /active:yes`) | T1564 |
| 08:21:19 | Process masquerading as LSM.exe | T1036.003 |
| 08:23:03 | Rundll32 setupapi.dll execution | T1218.011 |
| 08:23:46 | Masquerading as Windows LSASS process | T1036.003 |
| 08:24:43 | Read volume boot sector via DOS device path | T1006 |

## Phase 3 — Collection & Exfiltration (08:25 – 08:28)

| Time | Activity | MITRE |
|---|---|---|
| 08:25:23 | Stage sensitive files | T1074.001 |
| 08:26:14 | Stage sensitive files | T1074.001 |
| 08:26:55 | Stage sensitive files | T1074.001 |
| 08:27:45 | **Compress staged directory → `staged.zip`** | T1560.001 |
| 08:28:32 | **Exfiltrate `staged.zip` (155,287 bytes) → 192.168.67.128:8888** | T1041 |

## Continuous

| Activity | MITRE | Source |
|---|---|---|
| `POST /beacon` to 192.168.67.128:8888 (interval ~54s) | T1071 | PCAP |

## Timestamp Note

Operation report and Sysmon record UTC. The PCAP records local system time (first packet 11:16:41, last 12:48:40), which accounts for the offset between sources.

The LSASS access at 07:28:50 predates the first ability at 07:58:40 by ~30 minutes — consistent with `splunkd.exe` (first check-in 06:13:27) operating independently of the automated ability chain that ran later under the second agent.