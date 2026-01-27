# SOC Tools – Simple Working Principles & Flow (SIEM, SOAR, EDR, XDR)

This document gives a **clear, simple summary** of how SOC tools work, how they interact, and how **collection, detection, correlation, and response** happen in real environments.

---

## 1. What a SOC Does (Core Idea)

A SOC exists to:

**See → Understand → Stop → Record**

All SOC tools support one or more of these steps.

---

## 2. Four Core SOC Functions (Very Important)

| Function | Meaning |
|--------|--------|
| Collection | Getting security data |
| Detection | Finding suspicious activity |
| Correlation | Connecting related activity |
| Response | Stopping and containing attacks |

---

## 3. Data Collection (How data enters SOC)

### What data exists in a company
- User logins
- Web requests
- Firewall traffic
- Endpoint activity
- Email activity
- Cloud access

### Who collects what

- **SIEM** → collects logs (files, syslog, APIs)
- **EDR** → collects endpoint telemetry (agent-based)
- **XDR** → collects telemetry from multiple layers
- **SOAR** → does NOT collect logs continuously

---

## 4. Detection (How threats are found)

### SIEM Detection
- Rule-based
- Threshold and pattern matching
- Example: multiple failed logins

### EDR Detection
- Behavior-based
- Process, file, and memory behavior
- Example: PowerShell abuse

### XDR Detection
- Cross-layer behavior
- Email + endpoint + identity
- Example: phishing → malware → credential misuse

---

## 5. Correlation (Connecting the dots)

### What correlation means
Correlation means linking multiple events into **one attack story**.

### Where correlation happens
- **SIEM** → correlates logs (IP, user, time)
- **XDR** → correlates across layers (endpoint, email, identity)

Correlation reduces false alerts and shows real attacks.

---

## 6. Response (How attacks are stopped)

### EDR Response
- Kill process
- Quarantine file
- Isolate endpoint

### XDR Response
- Disable user
- Block domain/IP
- Contain attack within ecosystem

### SOAR Response
- Automates complex actions
- Blocks IP across firewalls
- Resets accounts
- Opens tickets
- Notifies teams

---

## 7. How SOC Tools Work Together (Flow)

```
Attacker / User Activity
        ↓
Logs & Endpoint Telemetry
        ↓
SIEM / EDR / XDR Detection
        ↓
Alert Created
        ↓
SOAR (If used)
        ↓
Automated / Manual Response
```

---

## 8. Role of Each SOC Tool (Simple)

| Tool | Main Role |
|----|----------|
| SIEM | Visibility & alerting |
| EDR | Endpoint protection |
| XDR | Cross-layer detection |
| SOAR | Automated response |

---

## 9. Simple Analogy (Easy to Remember)

- **SIEM** = CCTV cameras (see everything)
- **EDR** = Guard inside devices
- **XDR** = Investigator connecting clues
- **SOAR** = Emergency response team

---

## 10. Typical Company Usage

- Small company → EDR only
- Mid-size company → EDR + SIEM
- Mature SOC → SIEM + EDR + XDR + SOAR

---

## 11. Final Key Takeaway

- SIEM collects and alerts
- EDR detects and contains endpoint threats
- XDR connects attacks across layers
- SOAR automates and coordinates response

Together, these tools form a **complete SOC security workflow**.
