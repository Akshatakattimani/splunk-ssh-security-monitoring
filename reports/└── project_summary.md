# SSH Security Monitoring Project Summary

## Overview

This project demonstrates SSH security monitoring using Splunk Enterprise to analyze authentication events, monitor SSH activity, detect suspicious login attempts, and configure automated alerts for potential brute-force attacks.

---

## Objectives

- Analyze SSH authentication logs
- Monitor successful SSH logins
- Monitor failed SSH logins
- Identify top source IP addresses
- Identify top destination servers
- Create an SSH monitoring dashboard
- Configure brute-force detection alerts

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| SIEM | Splunk Enterprise |
| Virtualization | Oracle VirtualBox |
| Operating System | Kali Linux |
| Log Source | SSH Authentication Logs |
| Search Language | SPL |

---

## Dashboard Components

- Total SSH Events
- Successful SSH Sessions
- Failed SSH Sessions
- Top Source IP Addresses
- Top Destination Servers

---

## Detection Logic

The project uses SPL queries to:

- Analyze SSH authentication events
- Extract source and destination IP addresses
- Identify abnormal authentication patterns
- Detect brute-force attempts
- Support security investigations

---

## Alert Configuration

Alert Name

SSH Brute Force Detection

Alert Type

Scheduled Alert

Trigger Condition

Number of Results > 0

Purpose

Detect repeated failed SSH authentication attempts.

---

## Skills Demonstrated

- Splunk Enterprise
- SPL Query Development
- SSH Log Analysis
- Dashboard Development
- Security Monitoring
- Authentication Analysis
- Brute Force Detection
- Alert Configuration
- Incident Investigation

---

## Key Outcomes

- Successfully monitored SSH authentication activity.
- Built an interactive security dashboard.
- Configured automated brute-force detection.
- Improved visibility into SSH authentication events.
- Strengthened practical SOC analyst skills.

---

## Future Improvements

- Email alert notifications
- Threat intelligence integration
- Multi-server monitoring
- Correlation searches
- Splunk Enterprise Security (ES)

---

## Conclusion

This project demonstrates practical experience using Splunk Enterprise to monitor SSH authentication events, build security dashboards, detect brute-force attacks, and investigate authentication activity in a simulated SOC environment.
