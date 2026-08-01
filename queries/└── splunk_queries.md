# Splunk SSH Monitoring Queries

This document contains the Search Processing Language (SPL) queries used for SSH log analysis, dashboard creation, and brute-force detection in Splunk Enterprise.

---

# 1. Total SSH Events

## Objective

Determine the total number of SSH authentication events collected during the selected time period.

### SPL Query

```spl
index=main ssh
```

### Purpose

Retrieves all SSH authentication events from the `main` index.

### Security Significance

Provides an overall view of SSH activity. A sudden increase in SSH events may indicate heavy administrative activity or suspicious authentication attempts.

---

# 2. Successful SSH Sessions

## Objective

Identify successful SSH authentication events.

### SPL Query

```spl
index=main ssh success
| stats count AS "Successful SSH Sessions"
```

### Purpose

Counts successful SSH login events.

### Security Significance

Helps verify legitimate user access and compare successful logins with failed authentication attempts.

---

# 3. Failed SSH Sessions

## Objective

Identify failed SSH authentication attempts.

### SPL Query

```spl
index=main ssh failure
| stats count AS "Failed SSH Sessions"
```

### Purpose

Counts failed SSH login attempts.

### Security Significance

A high number of failed authentication events may indicate password guessing, brute-force attacks, or unauthorized access attempts.

---

# 4. Top Source IP Addresses

## Objective

Identify the IP addresses generating the highest number of SSH authentication events.

### SPL Query

```spl
index=main ssh
| rex field=_raw "^\S+\s+\S+\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)"
| top src_ip
```

### Purpose

Extracts the source IP address from the raw log using the `rex` command and ranks the IP addresses by event count.

### Security Significance

Helps identify scanners, attackers, or unusually active hosts.

---

# 5. Top Destination Servers

## Objective

Identify the servers receiving the highest number of SSH connection attempts.

### SPL Query

```spl
index=main ssh
| rex field=_raw "^\S+\s+\S+\s+\d+\.\d+\.\d+\.\d+\s+\d+\s+(?<dest_ip>\d+\.\d+\.\d+\.\d+)"
| top dest_ip
```

### Purpose

Extracts destination IP addresses from the raw SSH log and ranks the servers by authentication activity.

### Security Significance

Frequently targeted servers should be monitored closely because they may represent critical systems or preferred attacker targets.

---

# 6. SSH Brute Force Detection

## Objective

Detect possible brute-force attacks based on repeated failed SSH authentication attempts.

### SPL Query

```spl
index=main ssh failure
| rex field=_raw "^\S+\s+\S+\s+(?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| where count > 20
```

### Purpose

Identifies source IP addresses generating more than 20 failed SSH login attempts.

### Alert Configuration

| Setting | Value |
|---------|-------|
| Alert Type | Scheduled |
| Trigger Condition | Number of Results > 0 |
| Action | Add to Triggered Alerts |

### Security Significance

Repeated failed authentication attempts from the same source IP may indicate password guessing or brute-force attacks.

---

# Dashboard Panels

The SSH Security Monitoring Dashboard includes:

- Total SSH Events
- Failed SSH Logins
- Successful SSH Logins
- Top Source IP Addresses
- Top Destination Servers

These dashboard panels provide a centralized view of SSH authentication activity, enabling faster monitoring and investigation.

---

# Skills Demonstrated

- Splunk Search Processing Language (SPL)
- SSH Log Analysis
- Field Extraction using `rex`
- Dashboard Development
- Authentication Monitoring
- Brute-Force Detection
- Alert Configuration
- Security Monitoring
- Incident Investigation
