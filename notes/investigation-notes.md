# Investigation Notes

## Overview

This document records findings from the Apache Suspicious IP Investigation.

---

# Dataset Information

| Field | Value |
|---------|---------|
| Log Source | Apache Access Logs |
| SIEM | Splunk Enterprise |
| Index | main |

---

# Queries Executed

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

## Timeline Analysis

```spl
index=main
| timechart count by clientip limit=10
```

---

# Findings

## Total Events

```text
Document Results
```

## Most Active Source IP

```text
Document Results
```

## Most Requested Resources

```text
Document Results
```

## HTTP Methods Observed

```text
Document Results
```

## HTTP Status Codes Observed

```text
Document Results
```

## User-Agent Strings Observed

```text
Document Results
```

## Reconnaissance Indicators

```text
Document Results
```

---

# Analyst Assessment

Determine whether activity represents:

- Normal User Activity
- Search Engine Crawling
- Monitoring Activity
- Automated Scanning
- Reconnaissance Activity
- Potentially Malicious Behavior

---

# Conclusion

Summarize findings, determine overall risk level, and document recommended next investigative actions.
