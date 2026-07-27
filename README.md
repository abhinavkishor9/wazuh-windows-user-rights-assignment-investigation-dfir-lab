# wazuh-windows-user-rights-assignment-investigation-dfir-lab

## Overview

This Digital Forensics and Incident Response (DFIR) lab demonstrates how Windows User Rights Assignment changes can be investigated using native Windows Security logs and Wazuh.

Unlike Sysmon-based investigations, this lab relies entirely on Windows Security Event Logs, Event Viewer, PowerShell, Local Security Policy, and Wazuh Discover to detect and validate privilege assignment changes on a Windows endpoint.

The investigation also includes validating Windows Security auditing, confirming event ingestion through the Wazuh agent, and verifying evidence using both Windows-native tools and Wazuh Discover.

---

# Executive Summary

This investigation focused on detecting and validating Windows User Rights Assignment changes using native Windows Security Events and Wazuh.

The investigation included:

- Modifying Windows User Rights Assignment
- Generating Security Event IDs 4704 and 4705
- Validating events using Event Viewer
- Verifying events using PowerShell
- Confirming Wazuh agent connectivity
- Searching events using Wazuh Discover
- Verifying event ingestion through archives.json
- Correlating Windows Security logs with Wazuh alerts

The investigation demonstrates a structured DFIR workflow for validating privilege-related security changes before relying solely on SIEM data.

---

# Learning Objectives

- Understand Windows User Rights Assignment.
- Generate Security Event IDs 4704 and 4705.
- Validate Security events using Event Viewer.
- Verify events using PowerShell.
- Investigate authorization policy changes using Wazuh Discover.
- Confirm event ingestion through Wazuh.
- Correlate Windows Security events with SIEM alerts.

---

# Skills Demonstrated

- Windows DFIR Investigation
- Windows Security Log Analysis
- Privilege Change Investigation
- User Rights Assignment Analysis
- Event Viewer Analysis
- PowerShell Event Validation
- Wazuh Discover Investigation
- Windows Event Correlation
- Digital Evidence Documentation
- DFIR Troubleshooting
- MITRE ATT&CK Mapping

---

# Tools Used

- Wazuh Dashboard (Discover)
- Windows Event Viewer
- Windows PowerShell
- Local Security Policy (secpol.msc)
- Windows Security Event Log
- Wazuh Agent
- archives.json

---

# Lab Environment

| Component | Details |
|-----------|---------|
| SIEM | Wazuh 4.12 |
| Endpoint | Windows 11 Pro |
| Server | Oracle Linux 9 |
| Investigation Type | Windows DFIR |
| Event Source | Windows Security Log |
| Sysmon | Not Used |

---

# Investigation Scenario

A local administrator modified the **User Rights Assignment** policy on a Windows workstation by adding and later removing a user from the **"Shut down the system"** privilege.

As the DFIR analyst, the objectives were to determine:

- Whether the privilege assignment was successfully logged
- Which Windows Security Event IDs were generated
- Whether Wazuh collected the events
- Whether the Security logs and SIEM evidence matched
- How to validate event collection when investigating authorization policy changes

---

# Investigation Workflow

1. Verify Wazuh agent connectivity.
2. Confirm Windows Security auditing configuration.
3. Open Local Security Policy.
4. Modify a User Rights Assignment.
5. Generate Event ID 4704.
6. Remove the assigned privilege.
7. Generate Event ID 4705.
8. Validate events using Event Viewer.
9. Verify events using PowerShell.
10. Confirm event ingestion through archives.json.
11. Search events using Wazuh Discover.
12. Correlate investigative findings.
13. Document evidence.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Account Manipulation | T1098 |
| Privilege Escalation | Account Manipulation | T1098 |

### Why User Rights Assignment Investigations Matter

Changes to Windows User Rights Assignment can significantly alter a user's privileges on a system. Unauthorized privilege assignments may enable persistence, privilege escalation, or unauthorized administrative actions. Monitoring Security Events 4704 and 4705 allows analysts to detect and investigate these changes during incident response.

---

# Evidence Collected

- Windows Security Event Log
- Event IDs 4704 and 4705
- Local Security Policy configuration
- Event Viewer
- PowerShell validation
- Wazuh Discover searches
- Wazuh archives.json
- Wazuh Agent status

---

# Evidence Correlation

| Evidence Source | Information Obtained | Investigation Value |
|-----------------|---------------------|--------------------|
| Local Security Policy | Privilege modification | Activity performed |
| Event Viewer | Event IDs 4704 & 4705 | Primary evidence |
| PowerShell | Event validation | Independent verification |
| archives.json | Event ingestion | Manager validation |
| Wazuh Discover | Security alerts | SIEM correlation |

---

# Investigation Findings

- Windows successfully generated Security Event IDs 4704 and 4705 after modifying User Rights Assignment.
- Event generation was validated using both Event Viewer and PowerShell.
- The Wazuh agent successfully forwarded Windows Security events.
- Event ingestion was confirmed through archives.json.
- Wazuh Discover successfully indexed the authorization policy change events.
- The investigation demonstrated successful end-to-end correlation between Windows Security logs and Wazuh.

---

# Key Takeaways

- Windows Security Events 4704 and 4705 provide valuable evidence for privilege assignment investigations.
- Event Viewer and PowerShell should always be used to validate Windows event generation.
- archives.json is an effective method for confirming successful event ingestion into Wazuh.
- Wazuh Discover provides centralized visibility into authorization policy changes.
- Correlating multiple evidence sources improves DFIR accuracy and investigation confidence.

---
