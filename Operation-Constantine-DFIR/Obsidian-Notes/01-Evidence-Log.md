# Evidence Log

## Evidence Items

| ID | File | Size | Hash |
|----|------|------|------|
| E001 | windows machine-disk1.vmdk | 60 GB | MD5: `800db19a4cf11919951dff9707ab509f`<br>SHA1: `7d5e2f7490072f14d48d44b40e951f9b704e1116` |
| E002 | attacker operation report.json | 66 KB | SHA256: `B595B544DF149C3E6116F8A709D31661209B4F3CC1606F58050AD7CD6437D83A` |
| E003 | ConsoleHost_history.txt | 32 KB | SHA256: `DE9C4FC31F7A428FF23CB8AEDDC79D972EF545B55646FD9A8CB97E3AB58BF5A6` |
| E004 | NulltackKatz_v1.3.py | 32 KB | SHA256: `0FCF079A631B2E358E3B46B89A81E572879F26A79128F03FC1325F0D9028EBF0` |
| E005 | staged.zip | 152 KB | SHA256: `9AD0C149EA0751503FA0D76E420E793926A97049C0A783760E4C515477500A82` |
| E006 | 20_constantine_group_network_capture.pcapng | 24 MB | SHA256: `3da0ae422acf0e162b76916b8ec3fc7e0e08fd50ea752748739075de3cd014b3`<br>SHA1: `91ebdf01099f350f492c6e26c2e96b85fc74c0a1` |

## Disk Image Details

- Sector count: 125,829,120
- Bad blocks: None
- Partitions: EFI (100MB) · MSR (16MB) · Basic Data (60,798MB) · Recovery (522MB)
- Mounted read-only in FTK Imager 8.2.0.26

## PCAP Details

- Packets: 24,879
- First packet: 2026-07-05 11:16:41 (local time)
- Last packet: 2026-07-05 12:48:40 (local time)
- Elapsed: 01:31:59
- Interface: Ethernet0

## Key Artifact Locations

| Artifact | Path |
|---|---|
| Caldera agent | `C:\Users\Public\splunkd.exe` |
| Payload | `\Users\anmar\Desktop\20-Scenario\NulltackKatz_v1.3.py` |
| Staging directory | `C:\Windows\system32\staged` |
| Archive | `C:\Windows\system32\staged.zip` |
| Hidden account | `HKLM\SAM\Domains\Account\Users\Names\$` |
| PowerShell history | `\Users\anmar\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt` |
| Sysmon config | `\Sysmon\20_scenario_rules.xml` |

## Tools Used

FTK Imager 8.2.0.26 · Registry Explorer (Eric Zimmerman) · Event Viewer · Wireshark 4.6.6 · CyberChef · PowerShell Get-FileHash