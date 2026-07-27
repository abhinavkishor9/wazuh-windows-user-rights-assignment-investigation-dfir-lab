# Troubleshooting Notes

## Issue 1 — Event IDs 4704 and 4705 Not Generated

### Cause

Windows Security auditing for **Policy Change** or **Authorization Policy Change** was not configured, preventing User Rights Assignment events from being logged.

### Resolution

Verify the audit policy using:

```cmd
auditpol /get /category:"Policy Change"
```

If necessary, enable auditing:

```cmd
auditpol /set /subcategory:"Audit Policy Change" /success:enable
```

---

## Issue 2 — No Events Returned by PowerShell

### Cause

The initial PowerShell query searched only a limited number of Security events or filtered for Event IDs that had not yet been generated.

### Resolution

Increase the search range or query the Event IDs directly using `FilterHashtable`.

Example:

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4704
} -MaxEvents 5
```

Repeat for Event ID **4705**.

---

## Issue 3 — No Results in Wazuh Discover

### Cause

The User Rights Assignment events had not yet been indexed or the search was performed with an incorrect Event ID or time range.

### Resolution

Verify that the events exist in Windows Event Viewer first, then adjust the Discover time range and search for:

```text
data.win.system.eventID:4704
```

or

```text
data.win.system.eventID:4705
```

---

## Issue 4 — Event Viewer and Wazuh Discover Differ

### Cause

Windows generated the Security events successfully, but indexing into Discover required additional time.

### Resolution

Confirm successful ingestion using:

```bash
grep '"eventID":"4704"' \
/var/ossec/logs/archives/archives.json
```

Repeat for Event ID **4705** if required.

---

## Issue 5 — Verify Wazuh Agent Health

### Cause

If Security events do not appear in Discover, the Wazuh agent may not be communicating correctly with the manager.

### Resolution

Verify agent status:

```bash
sudo /var/ossec/bin/agent_control -i 001
```

Confirm:

- Agent Status: **Active**
- Latest Keep Alive updated
- Endpoint connected successfully

---

## Issue 6 — User Rights Assignment Change Not Logged

### Cause

Some User Rights Assignment modifications may not immediately generate the expected Security events if the policy change is not applied correctly.

### Resolution

Ensure the user is successfully added or removed through **Local Security Policy (secpol.msc)**, apply the change, then verify the corresponding Security events in Event Viewer before investigating Wazuh.

---

# Lessons Learned

- Always verify Windows Security auditing before generating User Rights Assignment events.
- Event Viewer is the authoritative source for validating Windows Security Events.
- PowerShell provides fast validation but depends on accurate filters and search ranges.
- Confirm event ingestion through **archives.json** before assuming an indexing issue in Discover.
- Wazuh Discover should be used after validating both Windows event generation and successful log ingestion.
- Correlating Local Security Policy, Event Viewer, PowerShell, archives.json, and Wazuh Discover provides a reliable DFIR workflow for investigating Windows authorization policy changes.
