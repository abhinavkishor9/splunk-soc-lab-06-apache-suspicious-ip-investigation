# splunk-soc-lab-06-apache-suspicious-ip-investigation

## Overview

This lab demonstrates how to investigate source IP activity using Apache access logs in Splunk Enterprise.

Source IP analysis is a critical SOC analyst task used to identify reconnaissance activity, automated scanning, abnormal traffic patterns, and potential attack sources. By analyzing request volumes, accessed resources, HTTP methods, status codes, and User-Agent strings, analysts can determine whether activity is legitimate or suspicious.

The objective of this lab is to identify high-volume source IPs, investigate their behavior, and assess potential security risks.

---

# Lab Environment

- Splunk Enterprise
- Search & Reporting App
- Apache Access Logs
- Windows Host

---

# Scenario

The SOC team has observed unusual web traffic patterns and wants to determine whether specific source IP addresses are performing reconnaissance or automated scanning activity against a web application.

As a SOC Analyst, your task is to identify suspicious IP addresses, investigate their activity, and determine whether further action is required.

---

# Objectives

- Identify top source IP addresses
- Analyze request volume
- Investigate accessed resources
- Review HTTP methods
- Review HTTP status codes
- Analyze User-Agent strings
- Detect reconnaissance indicators
- Develop IP-centric investigation skills

---

# MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1595 | Active Scanning |
| T1046 | Network Service Discovery |
| T1590 | Gather Victim Network Information |

---

# Severity

**Medium**

High-volume requests, excessive URL enumeration, or unusual access patterns may indicate reconnaissance or automated scanning activity.

---

# Detection Logic

## Top Source IP Addresses

```spl
index=main
| stats count by clientip
| sort -count
```

## Resources Accessed by a Specific IP

```spl
index=main clientip="<IP_ADDRESS>"
| stats count by uri
| sort -count
```

## HTTP Methods Used

```spl
index=main clientip="<IP_ADDRESS>"
| stats count by method
```

## HTTP Status Codes Generated

```spl
index=main clientip="<IP_ADDRESS>"
| stats count by status
```

## User-Agent Analysis

```spl
index=main clientip="<IP_ADDRESS>"
| stats count by useragent
```

## Reconnaissance Detection

```spl
index=main
| stats dc(uri) as unique_urls count by clientip
| sort -unique_urls
```

## Error Generation Analysis

```spl
index=main
| stats count by clientip status
| sort -count
```

## Timeline Analysis

```spl
index=main
| timechart count by clientip limit=10
```

---

# False Positives

- Search engine crawlers
- Vulnerability management scanners
- Monitoring tools
- Internal testing activity
- Load balancers
- High-volume legitimate users

---

# Recommended Containment

Validate suspicious source IP activity, review accessed resources, monitor ongoing behavior, and block confirmed malicious IPs when appropriate.

---

# Skills Demonstrated

- Splunk SPL
- Threat Hunting
- Apache Log Analysis
- Web Traffic Analysis
- IOC Investigation
- Security Monitoring
- Incident Investigation
- SOC Operations

---

# Lessons Learned

This lab improves understanding of:

- Source IP analysis
- Traffic profiling
- Reconnaissance detection
- Apache web log investigations
- Threat hunting methodologies
- Splunk search techniques
