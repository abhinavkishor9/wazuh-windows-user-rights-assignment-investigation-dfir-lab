# Investigation Notes

## Lab Summary

This investigation focused on analyzing Windows User Rights Assignment changes using native Windows Security logs and Wazuh Discover.

The investigation reconstructed privilege modification activity by correlating Local Security Policy, Windows Event Viewer, PowerShell, Wazuh Discover, and Wazuh archives to validate authorization policy changes.

---

## Analyst Methodology

The investigation followed a structured DFIR workflow:

1. Verify Wazuh agent connectivity.
2. Confirm Windows Security auditing configuration.
3. Modify Windows User Rights Assignment.
4. Generate Event ID 4704.
5. Remove the assigned privilege.
6. Generate Event ID 4705.
7. Validate events using Event Viewer.
8. Verify events using PowerShell.
9. Confirm event ingestion through archives.json.
10. Search Wazuh Discover.
11. Correlate evidence.
12. Document findings.

---

## Investigation Scenario

A Windows administrator modified the **"Shut down the system"** User Rights Assignment by adding and later removing a local user.

The investigation aimed to determine:

- Whether Windows generated User Rights Assignment events.
- Which Security Event IDs were created.
- Whether Wazuh successfully collected the events.
- Whether event ingestion could be validated independently.
- Whether Windows and Wazuh evidence correlated successfully.

---

## Evidence Collected

### Evidence 1 – Local Security Policy

Collected:

- User Rights Assignment configuration
- Added local user
- Removed local user

Finding:

Successfully generated Windows authorization policy changes for investigation.

---

### Evidence 2 – Windows Event Viewer

Collected:

- Windows Security Log
- Event ID 4704
- Event ID 4705

Finding:

Confirmed successful generation of User Rights Assignment events.

---

### Evidence 3 – PowerShell Validation

**Command Used**

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4704
} -MaxEvents 5

Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4705
} -MaxEvents 5
```

Finding:

PowerShell independently confirmed successful generation of Security Event IDs 4704 and 4705.

---

### Evidence 4 – Wazuh Discover

Collected:

- Security Event searches
- Authorization Policy Change events

Finding:

Confirmed that Wazuh indexed the User Rights Assignment activity.

---

### Evidence 5 – archives.json

Collected:

- Raw Windows Security events

Finding:

Confirmed successful ingestion of Windows Security Events by the Wazuh Manager before indexing into Discover.

---

## DFIR Analysis

The investigation demonstrated how Windows privilege modifications can be reconstructed using multiple evidence sources.

The workflow validated event generation in Windows before confirming successful collection by Wazuh. Correlating Local Security Policy, Event Viewer, PowerShell, archives.json, and Discover provided high confidence that the authorization policy changes were accurately recorded throughout the logging pipeline.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Account Manipulation | T1098 |
| Privilege Escalation | Account Manipulation | T1098 |

---

## Analyst Observations

- Windows Security Event IDs 4704 and 4705 provide reliable evidence of User Rights Assignment changes.
- Event Viewer remains the authoritative source for Windows Security events.
- PowerShell provides quick and independent event validation.
- archives.json is valuable for confirming successful event ingestion before relying on Discover.
- Wazuh Discover enables centralized investigation and correlation of authorization policy changes.
- Multiple evidence sources improve confidence and accuracy during DFIR investigations.

---

## Conclusion

The investigation successfully demonstrated how Windows User Rights Assignment changes can be detected, validated, and correlated using native Windows Security logging and Wazuh Discover. By combining Local Security Policy, Event Viewer, PowerShell, archives.json, and Wazuh, the investigation followed a structured DFIR methodology that ensured accurate reconstruction of privilege assignment activity.
