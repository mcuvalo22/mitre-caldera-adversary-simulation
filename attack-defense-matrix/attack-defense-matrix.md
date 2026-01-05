# Attack–Defense Matrix

This matrix maps executed MITRE ATT&CK techniques
to deployed security controls and detection results.

| ATT&CK Tactic | Technique | Target System | Detection Tool | Result |
|--------------|-----------|---------------|----------------|--------|
| Initial Access | Phishing / Payload | Windows 10 | Windows Defender | Detected |
| Lateral Movement | SMB / WMI | Domain Controller | Logs | Partially detected |
| Persistence | Scheduled Task | Windows | None | Not detected |

This matrix was used to evaluate the effectiveness
of defensive controls and identify security gaps.
