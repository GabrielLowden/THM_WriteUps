# SOC Incident Report Template

```markdown
# Security Incident Report

## Incident ID
INC-YYYY-XXXX

## Analyst
<Name>

## Date Detected
YYYY-MM-DD

## Severity
Low | Medium | High | Critical

## Status
Open | Investigating | Contained | Resolved

---

# 1. Incident Summary

Brief overview of the security incident.

Example:
A phishing campaign targeted employees and attempted to collect login credentials using a spoofed login page.

---

# 2. Detection Method

How the incident was discovered.

Examples:

- SIEM alert
- EDR detection
- IDS/IPS alert
- User report
- Threat hunting

Alert Details:

| Field | Value |
|------|------|
| Alert Name | |
| Detection Rule | |
| Detection Time | |

---

# 3. Affected Assets

List impacted systems or users.

| Asset | Type | IP Address | Owner |
|------|------|------------|------|
| | | | |

---

# 4. Indicators of Compromise (IOCs)

| Type | Value |
|-----|------|
| IP Address | |
| Domain | |
| URL | |
| File Hash | |
| Email Sender | |

---

# 5. Timeline of Events

Chronological record of the investigation.

| Time | Event |
|-----|------|
| | |
| | |
| | |

---

# 6. Investigation Details

Describe the analysis performed.

Examples:

- log review
- email header analysis
- endpoint investigation
- packet capture analysis

Tools used:

- SIEM
- EDR
- VirusTotal
- Wireshark
- Log analysis

Key findings:

- 
- 
- 

---

# 7. Impact Assessment

Determine the scope and impact.

Questions to consider:

- Were credentials compromised?
- Was malware executed?
- Was data exfiltrated?
- Were additional systems affected?

Impact summary:

---

# 8. Containment Actions

Steps taken to stop the threat.

Examples:

- blocked malicious IP/domain
- disabled compromised accounts
- quarantined affected endpoint
- removed malicious files

Actions taken:

- 
- 
- 

---

# 9. Eradication & Recovery

Steps taken to fully remove the threat and restore systems.

Examples:

- malware removal
- system patching
- password resets
- system restoration

---

# 10. Root Cause

Explain how the incident occurred.

Example:
User clicked a phishing email and entered credentials into a spoofed login page.

---

# 11. Lessons Learned

Recommendations to prevent future incidents.

- 
- 
- 

---

# 12. Evidence / References

Evidence collected:

- logs
- screenshots
- email samples
- PCAP files