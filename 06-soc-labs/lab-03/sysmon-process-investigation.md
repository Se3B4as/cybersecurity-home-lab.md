# EDR Lab 02 — Windows Process Investigation Using Sysmon and Wazuh

## 1. Objective

Investigate Windows process creation events using Microsoft Sysmon and Wazuh SIEM, focusing on process relationships, execution context, and the identification of potentially suspicious behavior.

The investigation aims to develop practical skills in endpoint monitoring, process analysis, event correlation, and evidence-based security assessment.

## 2. Lab Environment

- **Endpoint:** Windows 11 Home (PC2)
- **Monitoring Platform:** Wazuh SIEM
- **Endpoint Agent:** Wazuh Agent 4.14.10
- **Telemetry Source:** Microsoft Sysmon
- **Event Log:** `Microsoft-Windows-Sysmon/Operational`
- **Event ID:** `1 — Process Creation`
- **Investigation Tools:** Wazuh Dashboard and Windows PowerShell

## 3. Investigation Scenario

During endpoint monitoring in the Wazuh Dashboard, a Sysmon Event ID 1 was identified involving the execution of `net1.exe`.

The executable was launched by `net.exe` under the `NT AUTHORITY\SYSTEM` security context.

Because Windows account enumeration commands can be associated with both legitimate administrative activity and security-relevant reconnaissance, the event was selected for further investigation.

## 4. Evidence Collected

### Process Information

- **Event ID:** `1 — Process Creation`
- **Image:** `C:\Windows\SysWOW64\net1.exe`
- **Parent Image:** `C:\Windows\SysWOW64\net.exe`
- **User:** `NT AUTHORITY\SYSTEM`
- **Command Line:** Related to user account enumeration
- **Current Directory:** `C:\Program Files (x86)\ossec-agent\`

### Process Identifiers

**Child Process — net1.exe**

```text
ProcessGuid:
{517be7e5-6988-6afb-1006-000000006200}
```

**Parent Process — net.exe**

```text
ParentProcessGuid:
{517be7e5-6988-6afb-0e06-000000006200}
```

These identifiers were used to correlate the child process with its parent.

## 5. Investigation Methodology

### Step 1 — Event Identification

Accessed Wazuh Dashboard and filtered events by:

- Monitored Windows endpoint
- Microsoft Sysmon provider
- Event ID 1

Identified a process creation event involving `net1.exe`.

### Step 2 — Process Analysis

Examined the following Sysmon fields:

- `Image`
- `ParentImage`
- `CommandLine`
- `User`
- `CurrentDirectory`
- `ProcessGuid`
- `ParentProcessGuid`

The event indicated that `net1.exe` was initiated by `net.exe`.

### Step 3 — Execution Context Analysis

The process was executed under:

```text
NT AUTHORITY\SYSTEM
```

This is a privileged Windows system account commonly used by operating system components and services.

The working directory was associated with the installed Wazuh Agent.

This observation suggested a possible relationship with endpoint monitoring activity, although the originating application was not conclusively identified.

### Step 4 — Process Correlation

The investigation compared the child process's `ParentProcessGuid` with the `ProcessGuid` of its parent.

An initial search in Wazuh Threat Hunting did not return the parent process event.

A subsequent investigation was performed using Windows PowerShell and the local Sysmon event log.

The matching parent process GUID was located in the local event data.

However, the complete originating process chain was not established during this investigation.

## 6. PowerShell Investigation

The following command was used to search for the parent process in the local Sysmon event log:

```powershell
$parentGuid = '{517be7e5-6988-6afb-0e06-000000006200}'

Get-WinEvent -FilterHashtable @{
    LogName = 'Microsoft-Windows-Sysmon/Operational'
    Id = 1
} | Where-Object {
    $eventXml = [xml]$_.ToXml()

    $processGuid = $eventXml.Event.EventData.Data |
        Where-Object { $_.Name -eq 'ProcessGuid' }

    $processGuid.'#text' -eq $parentGuid

} | Select-Object -First 1 -ExpandProperty Message
```

The command searches local Sysmon process creation events using the parent process GUID.

The matching GUID was successfully located.

## 7. Process Relationship

The following process relationship was identified:

```text
Unknown Originating Process
          |
          v
       net.exe
          |
          v
      net1.exe
          |
          v
  User Account Enumeration
```

The relationship between `net.exe` and `net1.exe` was supported by Sysmon process metadata.

The originating process responsible for launching `net.exe` was not conclusively identified.

## 8. Security Analysis

The investigation identified several relevant observations.

**Indicators consistent with legitimate activity:**

- The executables were located in standard Windows directories.
- The `net.exe` and `net1.exe` relationship is consistent with normal Windows behavior.
- The execution occurred under a Windows system account.
- The working directory was associated with the installed Wazuh Agent.

**Factors requiring additional context:**

- User account enumeration can also occur during attacker reconnaissance.
- Execution under `NT AUTHORITY\SYSTEM` involves elevated privileges.
- The original process responsible for initiating the activity was not confirmed.
- Executable authenticity and the precise command-line arguments were not independently validated.

No evidence of malicious activity was established from the collected information.

However, the available evidence is insufficient to definitively classify the execution as benign.

## 9. Investigation Outcome

**Classification:** Inconclusive — likely legitimate system or monitoring-related activity.

**Confirmed findings:**

- Sysmon successfully recorded process creation events.
- Wazuh successfully displayed Sysmon Event ID 1 events.
- `net1.exe` was executed by `net.exe`.
- The execution occurred under `NT AUTHORITY\SYSTEM`.
- The command was related to user account enumeration.
- A matching parent process GUID was located in the local Sysmon logs.

**Limitations:**

- The originating process was not conclusively identified.
- The precise command-line arguments were not preserved in the report.
- No independent executable signature or hash verification was performed.
- The investigation did not establish whether the activity was initiated directly by Wazuh Agent.

**Final Assessment:**

The observed behavior is compatible with legitimate Windows administration or endpoint monitoring activity. No confirmed malicious indicators were identified, but the available evidence does not support a definitive benign classification.

## 10. Skills Developed

- Windows endpoint monitoring
- Microsoft Sysmon Event ID 1 analysis
- Wazuh SIEM event investigation
- Process creation analysis
- Parent-child process correlation
- Windows security context interpretation
- PowerShell event log investigation
- Evidence-based security reporting
- Recognition of investigation limitations

## 11. Key Takeaways

This lab demonstrated how Sysmon telemetry and Wazuh can be used together to investigate Windows process execution.

The investigation also highlighted the importance of correlating process identifiers, examining execution context, and avoiding conclusions based on a single event.

A legitimate Windows executable does not automatically imply legitimate activity, and the absence of confirmed malicious indicators does not establish that an event is harmless.

**Lab Status:** Completed — investigation documented with unresolved attribution.
