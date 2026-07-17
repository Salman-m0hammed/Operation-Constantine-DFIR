# Lessons Learned

## Documentation is not evidence

The task listed three techniques that did not exist in the data: T1547.001, T1134, and T1016. Each was checked and ruled out. Writing what the paperwork expects instead of what the evidence shows is how a report loses credibility. When they disagree, the evidence wins.

## Attackers hide from tools, not from sources

The `$` account is invisible to `net user` — Windows omits accounts ending in `$` from that output. But the account still has to exist in the SAM hive, because Windows has no other place to store it. Surface tools can be fooled; the underlying data source cannot.

## Absence is a finding

Proving the Run key was clean took checking three separate locations (HKLM, HKCU, Winlogon). That negative result is what made the T1564 conclusion defensible. "I didn't find it" is only worth something if you can show where you looked.

## Base64 is not encryption

The beacon traffic looked opaque, but it was Base64 — two layers of it. Decoding gave the actual C2 instruction the operator sent. Encoded traffic is worth a minute in CyberChef before assuming it's encrypted.

## Correlation is what makes a finding hold

Every key conclusion was confirmed from more than one source:
- Hidden account → operation report timestamp **and** SAM hive last-write time (both 08:20:22)
- Exfiltration → operation report ability **and** PCAP HTTP stream **and** matching file size on disk
- Agent identity → JSON `paw: qktity` **and** PCAP `X-Request-Id: DESKTOP-2A1O8LD-qktity`

## Logging config decides what survives

The attacker cleared event logs at 08:13:32. The LSASS evidence survived because Sysmon was configured with a `ProcessAccess` rule watching `lsass.exe` and the log had been captured. Detection depends on what you decided to record before the incident, not after.