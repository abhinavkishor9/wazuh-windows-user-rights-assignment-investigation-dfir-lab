# Troubleshooting Notes

## Issue 1

4704 not initially visible in Wazuh.

### Cause

Needed to verify Security auditing configuration.

### Resolution

Confirmed Audit Policy configuration and regenerated events.

---

## Issue 2

Needed confirmation that the agent received events.

### Resolution

Verified:

sudo /var/ossec/bin/agent_control -i 001

Agent status was Active.

---

## Issue 3

Needed confirmation that logs reached the manager.

### Resolution

Verified ingestion using:

archives.json

This confirmed successful event forwarding.

---

## Issue 4

Discover initially showed limited results.

### Resolution

Confirmed:

- Correct Event ID
- Correct time range
- Security log ingestion
- Successful indexing

---

## Validation Performed

✔ Windows Event Viewer

✔ PowerShell Get-WinEvent

✔ Agent Status

✔ archives.json

✔ Wazuh Discover

---

## Lessons Learned

- Always verify Windows event generation before troubleshooting Wazuh.
- archives.json is useful for confirming log ingestion.
- Agent connectivity should be verified before searching Discover.
- Windows Security auditing configuration directly impacts event availability.
