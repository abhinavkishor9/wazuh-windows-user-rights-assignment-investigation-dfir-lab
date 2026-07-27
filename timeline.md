# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 09:00 | Verified Wazuh agent connectivity | agent_control |
| 09:05 | Verified Windows Security auditing | auditpol |
| 09:10 | Opened Local Security Policy | secpol.msc |
| 09:15 | Modified User Rights Assignment | Local Security Policy |
| 09:18 | Generated Event ID 4704 | Windows Security Log |
| 09:22 | Removed assigned user right | Local Security Policy |
| 09:24 | Generated Event ID 4705 | Windows Security Log |
| 09:28 | Validated events using Event Viewer | Security Log |
| 09:32 | Verified events using PowerShell | Get-WinEvent |
| 09:36 | Confirmed agent connectivity | agent_control |
| 09:40 | Verified event ingestion | archives.json |
| 09:45 | Investigated Wazuh Discover | Discover |
| 09:50 | Correlated findings | Documentation |

---

# Investigation Flow

Investigation Started

↓

Verified Agent Health

↓

Verified Windows Security Auditing

↓

Modified User Rights Assignment

↓

Generated Event ID 4704

↓

Removed Assigned User Right

↓

Generated Event ID 4705

↓

Validated Using Event Viewer

↓

Verified Using PowerShell

↓

Confirmed Event Ingestion (archives.json)

↓

Investigated Wazuh Discover

↓

Correlated Evidence

↓

Investigation Completed

---

# Summary

The investigation reconstructed Windows User Rights Assignment activity using native Windows Security logs and Wazuh Discover. The lab demonstrated how privilege assignment changes generate Security Event IDs **4704** and **4705**, how those events can be validated using Event Viewer and PowerShell, and how successful log ingestion can be confirmed through **archives.json** before correlating the evidence in Wazuh Discover. The investigation reinforced a structured DFIR workflow by validating Windows event generation, confirming SIEM ingestion, and correlating multiple evidence sources to accurately investigate authorization policy changes.
