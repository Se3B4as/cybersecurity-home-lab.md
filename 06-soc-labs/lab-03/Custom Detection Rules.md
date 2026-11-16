# EDR Lab 03 — Custom Detection Rules with Wazuh and Sysmon

## 1. Objective

Develop, deploy, and validate a custom detection rule in Wazuh SIEM using Microsoft Sysmon process creation telemetry.

The goal was to identify executions of Windows `net.exe` and `net1.exe` and generate security alerts for further investigation.

## 2. Lab Environment

- **SIEM:** Wazuh 4.14.10
- **Server:** Ubuntu Server 24.04 LTS
- **Endpoint:** Windows 11 Home
- **Endpoint Monitoring:** Wazuh Agent and Microsoft Sysmon
- **Event Source:** Microsoft-Windows-Sysmon/Operational
- **Event ID:** 1 — Process Creation
- **Custom Rule ID:** 100100
- **Alert Level:** 6

## 3. Detection Scenario

Windows provides native command-line utilities for managing users, groups, and network resources.

Two relevant executables are:

- `net.exe`
- `net1.exe`

These utilities can be used for legitimate administrative operations but may also appear during security-relevant discovery activity.

The objective was to create a monitoring rule that identifies their execution without automatically classifying the activity as malicious.

## 4. Custom Detection Rule

The rule was added to:

`/var/ossec/etc/rules/local_rules.xml`

```xml
<group name="sysmon,windows,edr_lab,">

  <rule id="100100" level="6">
    <if_group>sysmon_event1</if_group>
    <field name="win.eventdata.image" type="pcre2">(?i)\\net1?\.exe$</field>
    <description>EDR Lab 03: Windows net.exe or net1.exe process execution detected</description>
    <group>process_creation,account_discovery,</group>
  </rule>

</group>
```

### Rule Explanation

- **Rule ID 100100:** Unique identifier for the custom detection.
- **Level 6:** Configured alert severity.
- **if_group:** Limits evaluation to the relevant Sysmon process creation event group.
- **win.eventdata.image:** Identifies the executable involved.
- **PCRE2:** Provides regular expression matching.
- **Case-insensitive matching:** Supports executable paths with different letter casing.

The rule detects process execution, not necessarily malicious behavior.

## 5. Deployment Procedure

### Step 1 — Back Up Existing Rules

```bash
sudo cp /var/ossec/etc/rules/local_rules.xml /var/ossec/etc/rules/local_rules.xml.bak
```

### Step 2 — Edit Local Rules

```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```

The custom rule was inserted into a new XML group.

### Step 3 — Validate Configuration

```bash
sudo /var/ossec/bin/wazuh-analysisd -t
```

The validation completed without reported configuration errors.

### Step 4 — Restart Wazuh Manager

```bash
sudo systemctl restart wazuh-manager
```

### Step 5 — Verify Service Status

```bash
sudo systemctl status wazuh-manager --no-pager
```

The service returned:

```text
Active: active (running)
```

## 6. Detection Test

A controlled test was performed on the Windows endpoint using:

```powershell
net user
```

This command queries local Windows accounts without modifying them.

Sysmon recorded the resulting process activity, and Wazuh evaluated the events against the custom rule.

## 7. Results

The Wazuh Dashboard displayed two alerts associated with Rule ID 100100.

### Confirmed Findings

- **Rule ID:** 100100
- **Alert Level:** 6
- **Endpoint:** PC2-WINDOWS11
- **Detected Executables:** net.exe and net1.exe
- **Event Source:** Microsoft Sysmon
- **Event ID:** 1

## 8. Security Analysis

The custom rule successfully identified process executions involving Windows network administration utilities.

However, the detection was intentionally broad.

For example, both account queries and ordinary help commands could trigger the same rule.

This behavior demonstrated the need for additional detection logic to distinguish specific security-relevant operations from general executable activity.

## 9. Outcome

**Status: Successfully validated**

The laboratory demonstrated the complete detection pipeline:

Windows Endpoint → Microsoft Sysmon → Wazuh Agent → Wazuh Manager → Custom Detection Rule → Wazuh Dashboard.

The rule generated the expected alerts during the controlled test.

## 10. Skills Developed

- Wazuh custom rule development
- XML rule configuration
- Microsoft Sysmon event analysis
- Windows process monitoring
- PCRE2 regular expressions
- SIEM rule validation
- Alert verification
- Detection engineering fundamentals

## 11. Key Takeaways

Custom SIEM rules can transform endpoint telemetry into actionable monitoring alerts.

However, detecting an executable is different from detecting a specific behavior.

This laboratory established the foundation for a follow-up exercise focused on improving detection precision through command-line analysis.

**Final Result:** Custom Rule 100100 successfully deployed and validated.
