# wazuh-windows-user-rights-assignment-investigation-dfir-lab
## Overview

This DFIR lab demonstrates how Wazuh can monitor Windows User Rights Assignment changes through native Windows Security Events.

The investigation focuses on detecting:

- User rights assigned
- User rights removed
- Authorization Policy Change events
- Windows Security Event IDs 4704 and 4705
- Verification of event ingestion inside Wazuh Discover

Unlike process-based investigations, this lab focuses on privilege modifications performed through Local Security Policy.

---

## Lab Objectives

- Understand Windows User Rights Assignment
- Generate Event ID 4704
- Generate Event ID 4705
- Validate Windows Event Viewer logs
- Verify event ingestion by the Wazuh agent
- Search and investigate events using Wazuh Discover
- Correlate Windows Security logs with Wazuh alerts

---

## Environment

**SIEM**
- Wazuh 4.12

**Endpoint**
- Windows 11 Pro

**Manager**
- Oracle Linux 9

---

## Windows Events Investigated

| Event ID | Description |
|----------|-------------|
|4704|A user right was assigned|
|4705|A user right was removed|

---

## Investigation Workflow

1. Configure Windows auditing.
2. Open Local Security Policy.
3. Modify User Rights Assignment.
4. Generate Event ID 4704.
5. Remove the assigned privilege.
6. Generate Event ID 4705.
7. Verify events in Windows Event Viewer.
8. Confirm ingestion through archives.json.
9. Search events in Wazuh Discover.
10. Validate alert correlation.

---

## Key Findings

- Windows successfully generated Event IDs 4704 and 4705.
- Wazuh agent collected Windows Security Events.
- Events were ingested into the Wazuh Manager.
- Discover successfully displayed Event ID 4704.
- Archives confirmed complete log collection.
- Event correlation between Windows and Wazuh was successful.

---

## Skills Demonstrated

- Windows DFIR
- Windows Security Event Analysis
- Wazuh Discover
- Privilege Change Investigation
- Windows Auditing
- Event Correlation
- Log Validation
- Security Monitoring

---

## MITRE ATT&CK

**T1098 — Account Manipulation**

Privilege assignments can indicate attempts to establish persistence or elevate access.

---

## Outcome

This investigation demonstrated how Windows privilege assignments can be monitored using native Windows Security Events and correlated within Wazuh Discover for DFIR investigations.
