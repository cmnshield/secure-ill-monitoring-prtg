#Secure ILL Monitoring & SLA Reporting with PRTG
Overview

This project documents the design and implementation of a secure, SLA-grade Internet Leased Line (ILL) monitoring solution using PRTG Network Monitor.

The implementation focuses on:

Accurate ISP uptime/downtime tracking

Least-privilege security design

Audit-ready monitoring and alerting

Noise-free, management-friendly reporting

🎯 Objectives

Monitor ILL availability (uptime & downtime) reliably

Generate SLA-ready reports for ISP performance validation

Implement monitoring access using security best practices

Avoid over-monitoring and reduce alert fatigue

🏗️ Architecture Overview

Monitoring Approach

Ping-based availability checks for SLA accuracy

SNMP-based WAN traffic monitoring for bandwidth visibility

Centralized monitoring via a single internal PRTG server

High-level flow

PRTG Server
   │
   ├── ICMP (Ping) → ISP Gateway (ILL Availability)
   └── SNMP (Read-only) → Firewall WAN Interface (Traffic)

🔐 Security Design Principles
Least Privilege

SNMP access configured as read-only

Monitoring restricted to a single internal PRTG server IP

Firewall rules tightly scoped (no ANY–ANY rules)

Network Security Controls

Allowed protocols:

ICMP (availability monitoring)

SNMP v2c (UDP 161, read-only)

SNMP not exposed on WAN interfaces

No inbound internet access to PRTG server

🔧 Implementation Summary
Firewall Configuration

Created explicit firewall rules allowing:

ICMP from PRTG server to monitored targets

SNMP (UDP 161) from PRTG server to network devices

Rules documented and managed via change management process

PRTG Configuration

Auto-discovery disabled to prevent sensor sprawl

Dedicated monitoring group for ILL links

Sensors used:

Ping Sensor → SLA source of truth

SNMP Traffic Sensor → WAN bandwidth & utilization

Alerting configured with delay thresholds to avoid false positives

🚨 Alerting Strategy

ISP outage alerts triggered only after sustained downtime

Recovery notifications sent when link stabilizes

No repeated alert spam

Alerts scoped strictly to ILL availability sensors

📊 Reporting & SLA Validation

Uptime and downtime automatically calculated by PRTG

Monthly SLA reports generated using uptime-based templates

Reports exported in PDF format for:

Management review

ISP escalation

Audit evidence

🧪 Testing & Validation

Verified ICMP reachability from PRTG to ISP gateway

Validated SNMP polling and traffic data collection

Simulated link outage to confirm alerting behavior

Confirmed no impact to production traffic

📋 Audit & Compliance Considerations

Firewall changes documented via formal change requests

Backup and rollback plans defined

Monitoring access traceable and reviewable

Design aligned with common audit expectations (ISO 27001-style controls)

✅ Outcomes

Accurate ILL uptime/downtime visibility

SLA-ready reporting without manual intervention

Secure monitoring with minimal attack surface

Clean, maintainable monitoring structure

⚠️ Notes

All IP addresses, hostnames, and provider names are anonymized

This repository focuses on design and security considerations, not vendor-specific secrets
