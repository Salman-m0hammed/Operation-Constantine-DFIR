# MITRE ATT&CK Techniques — 26 Confirmed

## Discovery (7)

| ID | Name | Evidence |
|---|---|---|
| T1033 | System Owner/User Discovery | `$env:username` — 07:58:40Z |
| T1087.001 | Account Discovery: Local Account | `Get-WmiObject -Class Win32_UserAccount` — 07:59:25Z |
| T1057 | Process Discovery | Find user processes — 08:00:35Z |
| T1135 | Network Share Discovery | View admin shares — 08:01:17Z |
| T1018 | Remote System Discovery | Discover domain controller — 08:02:10Z |
| T1518.001 | Security Software Discovery | Antivirus 08:02:58Z · Firewalls 08:04:42Z |
| T1069.001 | Permission Groups Discovery: Local Groups | 08:04:29Z |

## Credential Access (1)

| ID | Name | Evidence |
|---|---|---|
| T1003.001 | OS Credential Dumping: LSASS Memory | Sysmon EID 10 — `splunkd.exe` → `lsass.exe`, GrantedAccess `0x1FFFFF` — 07:28:50Z. Mimikatz also downloaded per PowerShell history. |

## Collection (3)

| ID | Name | Evidence |
|---|---|---|
| T1005 | Data from Local System | Find files ×3 — 08:05:44Z – 08:07:13Z |
| T1074.001 | Local Data Staging | staging dir 08:07:49Z; Stage sensitive files ×3 — 08:25–08:26Z |
| T1560.001 | Archive via Utility | `Compress-Archive` → staged.zip — 08:27:45Z |

## Defense Evasion / Stealth (11)

| ID | Name | Evidence |
|---|---|---|
| T1070.003 | Clear Command History | 08:08:37Z, 08:09:44Z |
| T1562.001 | Disable or Modify Tools | Disable Windows Defender — 08:10:47Z |
| T1222.001 | File Permissions Modification | Full Access to Everyone — 08:11:40Z |
| T1070.001 | Clear Windows Event Logs | 08:13:32Z |
| T1686 | Disable Firewall | 08:14:19Z |
| T1564.001 | Hidden Files and Directories | `attrib.exe +h` — 08:15:00Z |
| T1112 | Modify Registry | ExecutionPolicy → Bypass — 08:15:58Z |
| T1036.007 | Masquerading: Double Extension | 08:16:52Z |
| T1564.003 | Hidden Window | 08:17:55Z |
| T1036.003 | Rename System Utilities | 08:18:43Z · LSM.exe 08:21:19Z · LSASS 08:23:46Z |
| T1070 | Indicator Removal | FSUtil — 08:19:42Z |
| T1564 | **Hide Artifacts** | Hidden user `$` — 08:20:22Z |

## Execution (3)

| ID | Name | Evidence |
|---|---|---|
| T1059.001 | PowerShell | Move PowerShell & triage — 08:12:41Z |
| T1218.011 | Signed Binary Proxy: Rundll32 | `rundll32 setupapi.dll` — 08:23:03Z |
| T1006 | Direct Volume Access | Boot sector via DOS device path — 08:24:43Z |

## C2 & Exfiltration (2)

| ID | Name | Evidence |
|---|---|---|
| T1071 | Application Layer Protocol | `POST /beacon` → 192.168.67.128:8888, UA `Go-http-client/1.1` |
| T1041 | Exfiltration Over C2 Channel | `POST /file/upload` — staged.zip (155,287 bytes) — 08:28:32Z |

---

## Present in Payload, Not Executed

| ID | Name | Status |
|---|---|---|
| T1566.001 | Spearphishing Attachment | `phase1_spearphishing()` function in `NulltackKatz_v1.3.py` — email template: *"URGENT: Payroll System Security Update Required"* from `security@payroll-update.com`. Not executed by the Caldera operation. |
| T1204.002 | User Execution: Malicious File | `py .\NulltackKatz_v1.3.py` in PowerShell history |

## Expected but Not Observed

| ID | Name | Verification |
|---|---|---|
| T1547.001 | Registry Run Keys | HKLM Run · HKCU Run (NTUSER.DAT) · Winlogon — all clean |
| T1134 | Access Token Manipulation | Absent from all 35 abilities. Agent deployed at `privilege: Elevated` — no escalation required. |
| T1016 | System Network Config Discovery | Absent. Network discovery done via T1135 and T1018 instead. |

## Decoded C2 Instruction

Base64 beacon payload decoded (CyberChef):
```json
{"paw": "qktity", "sleep": 54, "instructions": [{
  "command": "<base64>", "executor": "psh", "delete_payload": true
}]}
```

Inner command decoded:
```powershell
Get-ChildItem C:\Users -Recurse -Include *.wav -ErrorAction 'SilentlyContinue' | foreach {$_.FullName} | Select-Object -first 5
```

The `paw` value matches the agent ID in the operation report. `delete_payload: true` shows the agent removes its own payloads after execution — anti-forensics.