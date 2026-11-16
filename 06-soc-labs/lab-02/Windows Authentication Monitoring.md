# SOC Lab 02 — Windows Authentication Monitoring

## Objective

Investigate Windows authentication events collected by Wazuh SIEM, correlate successful logon and logoff records, and evaluate whether the observed activity presents indicators of suspicious behavior.

## Lab Environment

- **SIEM:** Wazuh 4.14.10
- **Operating System:** Windows 11
- **Monitored Endpoint:** PC2
- **Log Source:** Windows Security Event Log
- **Analysis Platform:** Wazuh Threat Hunting

## Investigation Methodology

1. Identified a successful authentication event (Event ID 4624).
2. Examined the authentication type and associated account.
3. Reviewed the source IP address and authentication package.
4. Identified the Windows process associated with the event.
5. Located a logoff event (Event ID 4634).
6. Compared the Logon IDs and agent identifiers.
7. Verified the chronological order using the original event timestamps.
8. Searched for Event ID 6005 between the authentication and logoff events.

## Evidence Collected

- **Event ID:** `4624`
- **Logon Type:** `3 — Network`
- **Source IP:** Monitored endpoint's private IP
- **Target User:** Known Windows user
- **Subject User:** Known Windows user
- **Authentication Package:** `Negotiate`
- **LM Package Name:** Not identified
- **Workstation Name:** Not available
- **Process Name:** `C:\Windows\System32\services.exe`
- **Target Logon ID:** Hexadecimal identifier observed
  
### Event Correlation

A Windows Event ID 4634 was identified with the same Logon ID and Wazuh agent ID as the investigated Event ID 4624.

Comparison of the original Windows event timestamps confirmed that Event ID 4624 occurred before Event ID 4634.

No Event ID 6005 was found between the two timestamps in the available Wazuh results.

These findings support a possible relationship between the authentication and logoff events.

## Security Assessment

The observed activity is consistent with a potentially legitimate Windows network authentication.

Supporting observations:

- The source IP matched the monitored Windows endpoint.
- The authenticated account was recognized.
- The reported process was a standard Windows service-management executable.
- The authentication and logoff events shared a Logon ID.
- The original timestamps followed the expected chronological sequence.

No clear indicators of compromise were identified in the reviewed fields.

## Limitations

- The specific service responsible for the authentication was not identified.
- The authentication package did not establish which underlying protocol was ultimately selected.
- The absence of Event ID 6005 does not conclusively exclude a restart or a logging gap.
- Complete log collection continuity was not independently verified.
- The investigation was limited to the available event records.

## Conclusion

**Assessment:** Likely legitimate activity; not conclusively verified.

The investigation demonstrated successful event filtering, Windows authentication analysis, Logon ID correlation, timestamp validation, and evidence-based SOC triage.

No confirmed security incident was identified.

## Skills Practiced

- SIEM event investigation
- Windows Security Event analysis
- Authentication monitoring
- Log correlation
- Timeline validation
- SOC triage and documentation
- Evidence-based security assessment

## Status

**Completed — Preliminary security assessment documented.**
