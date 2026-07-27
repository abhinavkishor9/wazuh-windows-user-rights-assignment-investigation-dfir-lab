# Investigation Notes

## Objective

Investigate Windows User Rights Assignment changes using Wazuh.

---

## Events Investigated

4704

A user right was assigned.

4705

A user right was removed.

---

## Windows Activity

Opened:

Local Security Policy

↓

Local Policies

↓

User Rights Assignment

↓

Modified:

Shutdown the system

↓

Added local user

↓

Removed local user

---

## Event Verification

Verified in:

Windows Event Viewer

Windows Security Log

Generated:

4704

4705

---

## Wazuh Verification

Confirmed:

- Agent online
- Security log ingestion
- Event forwarding
- Discover indexing

---

## Evidence Collected

Windows Event Viewer

PowerShell

Get-WinEvent

Local Security Policy screenshots

Wazuh Discover

archives.json verification

---

## Correlation

Windows Security Log

↓

Wazuh Agent

↓

Wazuh Manager

↓

archives.json

↓

Alerts

↓

Discover

---

## Result

User Rights Assignment changes were successfully detected and investigated using Wazuh Discover.
