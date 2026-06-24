# Troubleshooting Notes

## Overview

This document records troubleshooting performed during the Apache Suspicious IP Investigation.

---

# Issue 1

## Problem

No results returned for:

```spl
index=main
| stats count by clientip
```

## Cause

Field extraction issue or incorrect field name.

## Resolution

Verify available fields:

```spl
index=main
| fieldsummary
```

Confirm that the field `clientip` exists.

---

# Issue 2

## Problem

No results returned for:

```spl
index=main clientip="<IP_ADDRESS>"
```

## Cause

Placeholder value was not replaced with an actual IP address.

## Resolution

Run:

```spl
index=main
| stats count by clientip
| sort -count
```

Select a valid IP address and rerun the query.

---

# Issue 3

## Problem

No results returned for User-Agent analysis.

```spl
index=main
| stats count by useragent
```

## Cause

Field extraction issue.

## Resolution

Review sample events:

```spl
index=main
| head 20
```

Verify field names in Interesting Fields.

---

# Issue 4

## Problem

Timeline analysis returns no data.

## Cause

Incorrect time range selected.

## Resolution

Set the Splunk time picker to:

```text
All Time
```

and rerun the search.

---

# Issue 5

## Problem

Unexpectedly high URL counts from a source IP.

## Cause

Search engine crawler, monitoring tool, or automated activity.

## Resolution

Review User-Agent strings and accessed resources before determining malicious intent.

---

# Verification Queries

## Verify Event Count

```spl
index=main
| stats count
```

## Verify Source

```spl
index=main
| stats count by source
```

## Verify Sourcetype

```spl
index=main
| stats count by sourcetype
```

## Verify Available Fields

```spl
index=main
| fieldsummary
```

## Review Sample Events

```spl
index=main
| head 20
```

---

# Lessons Learned

- Validate field availability before starting investigations.
- High request volume alone does not indicate malicious activity.
- User-Agent analysis provides important investigation context.
- Reconnaissance detection requires multiple indicators.
- Verification is a critical first step in every SOC investigation.
