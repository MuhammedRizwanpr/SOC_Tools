# SIEM, SOAR, EDR, and XDR – Complete Practical Overview

This document explains **what SIEM, SOAR, EDR, and XDR are**, **how they work**, **what data they collect**, **how response happens**, **where they are used**, and **how they work together** in real companies.

---

## 1. SIEM (Security Information and Event Management)

### What it is
SIEM is a **central log collection and monitoring system** used to detect security incidents by analyzing logs and events.

### What data SIEM collects
- Authentication logs (Windows, Linux, AD, VPN)
- Firewall logs
- Web server logs (Apache, Nginx, IIS)
- Network device logs
- DNS logs
- Cloud and application logs
- Alerts from EDR, IDS, antivirus

### How SIEM works
1. Logs are collected from configured sources (agents, syslog, APIs)
2. Logs are parsed and normalized
3. Correlation rules analyze behavior
4. Alerts are generated when rules match

### How SIEM takes response
- Sends alerts to SOC analysts
- Can notify via email, dashboard, ticket
- Can forward alerts to SOAR

### Where SIEM is needed
- Central visibility
- Threat detection
- Compliance and auditing
- SOC monitoring

### Common SIEM platforms
- Splunk Enterprise / Splunk ES
- IBM QRadar
- Elastic Security
- Microsoft Sentinel

---

## 2. SOAR (Security Orchestration, Automation, and Response)

### What it is
SOAR is an **automation and response platform** that acts after alerts are generated.

### What data SOAR receives
- Alerts from SIEM
- Alerts from EDR / XDR
- Contextual data (on demand)

### How SOAR works
1. Receives an alert
2. Executes a playbook
3. Enriches alert with context (IP reputation, asset info)
4. Takes automated or semi-automated action

### How SOAR takes response
- Block IP on firewall
- Disable user account
- Isolate endpoint
- Create tickets
- Send notifications

### What SOAR does NOT do
- Continuous log collection
- Endpoint monitoring

### Where SOAR is needed
- High alert volume
- Repetitive response tasks
- Large or mature SOCs

### Common SOAR platforms
- Palo Alto Cortex XSOAR
- Splunk SOAR
- IBM QRadar SOAR

---

## 3. EDR (Endpoint Detection and Response)

### What it is
EDR provides **endpoint-level detection, investigation, and response**.

### What EDR collects
- Process execution
- File creation and deletion
- Network connections by process
- Command-line activity
- Registry and memory behavior

### How EDR works
1. EDR agent runs on each endpoint
2. Agent monitors system activity
3. Suspicious behavior is detected
4. Alert is sent to EDR console

### How EDR takes response
- Kill malicious process
- Quarantine file
- Isolate endpoint
- Block hash, IP, or domain

### Where EDR is needed
- Malware and ransomware protection
- Endpoint visibility
- Incident containment

### Common EDR platforms
- Microsoft Defender for Endpoint
- CrowdStrike Falcon
- SentinelOne

---

## 4. XDR (Extended Detection and Response)

### What it is
XDR extends EDR by **correlating security data across multiple layers**.

### What XDR collects
- Endpoint telemetry (EDR)
- Email security events
- Identity and login events
- Network metadata
- Cloud and SaaS activity

### How XDR works
1. Collects telemetry from multiple layers
2. Normalizes data into a common format
3. Correlates related events
4. Creates a single incident

### How XDR takes response
- Endpoint isolation
- Block IP/domain
- Disable user
- Trigger SOAR for complex actions

### Where XDR is needed
- Advanced threat detection
- Cross-layer attacks
- Reduced alert noise

### Common XDR platforms
- Microsoft Defender XDR
- Palo Alto Cortex XDR

---

## 5. Working Flow (Simple)

```
Logs & Telemetry
     ↓
SIEM / EDR / XDR Detection
     ↓
Alerts
     ↓
SOAR (Automation)
     ↓
Response Actions
```

---

## 6. Comparison Table

| Technology | Main Role | Collects Logs | Detects | Responds | Automation |
|----------|----------|---------------|---------|----------|------------|
| SIEM | Central monitoring | Yes | Yes | Limited | No |
| SOAR | Automation | No | No | Yes | Yes |
| EDR | Endpoint protection | Endpoint only | Yes | Yes | Limited |
| XDR | Cross-layer detection | Telemetry | Yes | Yes | Some |

---

## 7. How They Work Together

- SIEM provides visibility
- EDR protects endpoints
- XDR correlates attacks across layers
- SOAR automates response

### Typical combinations
- Small company: EDR only
- Mid-size company: EDR + SIEM
- Mature SOC: SIEM + EDR + XDR + SOAR

---

## 8. Key Takeaway

- SIEM = Logs and alerts
- EDR = Endpoint security
- XDR = Attack correlation
- SOAR = Automated response

Together, they form a **complete SOC security architecture**.

