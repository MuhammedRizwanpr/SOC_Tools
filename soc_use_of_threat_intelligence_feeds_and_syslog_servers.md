# Use of Threat Intelligence Feeds and Syslog Servers in SOC

## 1. Purpose in SOC
Security Operations Centers (SOCs) need **visibility** (what is happening) and **context** (is it malicious). Syslog servers provide visibility by collecting logs, while Threat Intelligence (TI) feeds provide context by identifying known malicious indicators. Together, they enable faster detection, investigation, and response.

---

## 2. Syslog Server in SOC

### 2.1 What a Syslog Server Does
A syslog server is a **central log collection point**. It receives event-based logs from devices and systems, stores or buffers them, and forwards them to the SIEM.

### 2.2 Why SOC Uses a Syslog Server
- Centralized log collection
- Near real-time visibility
- Log buffering if SIEM is unavailable
- Log filtering and normalization
- Reduced SIEM ingestion cost
- Scalability and reliability

### 2.3 How Logs Reach the Syslog Server
- Devices act as **syslog clients**
- Logs are sent when events occur (event-driven)
- Transport protocols:
  - UDP 514 (fast, may lose logs)
  - TCP 514 (reliable)
  - TCP 6514 (TLS encrypted, secure)

### 2.4 Types of Logs Collected via Syslog
- **Security logs**: authentication success/failure, firewall allow/deny, IDS/IPS alerts, VPN events
- **Network logs**: connection attempts, session start/stop, routing changes
- **System logs**: service start/stop, reboots, kernel warnings
- **Application logs**: web access logs, app errors, database logins
- **Audit logs**: admin actions, configuration changes, file access

> Note: Syslog does NOT carry raw packets or file contents. It carries event metadata only.

---

## 3. Threat Intelligence (TI) Feeds in SOC

### 3.1 What Threat Intelligence Provides
Threat Intelligence feeds supply **Indicators of Compromise (IOCs)** and contextual data about known threats.

### 3.2 Types of Data from TI Feeds
- Malicious IP addresses
- Suspicious or malicious domains
- URLs (phishing, malware hosting)
- File hashes (MD5, SHA1, SHA256)
- Email senders
- Command-and-Control (C2) infrastructure
- Confidence scores, tags, and timestamps (depending on feed)

### 3.3 What TI Feeds Do NOT Provide
- They do not generate logs
- They do not monitor systems
- They do not block attacks by themselves

---

## 4. How Threat Intelligence Feeds Reach the SIEM

### 4.1 Ingestion Methods
Threat intelligence does **not** use syslog. It is ingested using:
- Built-in SIEM connectors
- API / HTTPS pull
- Webhooks or push from a Threat Intelligence Platform (TIP)

### 4.2 Fetching Process
1. SIEM authenticates to TI provider (API key/token)
2. SIEM periodically pulls IOC data (e.g., every 15–60 minutes)
3. IOCs are stored as:
   - Lookup tables
   - Reference sets
   - Threat lists
4. Old or expired indicators are removed automatically

### 4.3 Update Nature
- Scheduled, not event-driven
- Frequency depends on feed quality and SOC tuning

---

## 5. Combined Working Flow in SOC

### 5.1 End-to-End Flow
1. Endpoint / firewall / server generates an event
2. Event log is sent to the syslog server
3. Syslog server stores and forwards logs to SIEM
4. SIEM parses and normalizes logs
5. SIEM extracts indicators (IP, domain, hash)
6. Extracted indicators are compared with TI feed data
7. Match found → alert generated
8. SOC analyst investigates and responds

### 5.2 Visual Flow (Conceptual)
Devices → Syslog Server → SIEM → TI Enrichment → Alert → Response

---

## 6. How This Helps SOC Operations

### 6.1 Detection
- Faster identification of known threats
- Real-time alerting based on live events

### 6.2 Investigation
- Enriched alerts with threat context
- Reduced analyst investigation time

### 6.3 Response
- Prioritized alerts
- Automated blocking via SOAR (if integrated)

### 6.4 Operational Benefits
- Reduced false positives with tuned feeds
- Better visibility across infrastructure
- Improved compliance and audit readiness

---

## 7. Key Differences (Quick Reference)

| Aspect | Syslog Server | Threat Intelligence Feed |
|-----|-------------|--------------------------|
| Role | Log transport & collection | Context & enrichment |
| Data Type | Event-based logs | IOCs & metadata |
| Timing | Near real-time | Scheduled updates |
| Source | Internal devices | External providers |
| Analysis | No | Used by SIEM |

---

## 8. SOC Interview Summary
Syslog servers provide centralized, near real-time collection of security, network, system, and application logs, while threat intelligence feeds supply external indicators of known malicious activity. SIEM combines both by correlating incoming logs with threat intelligence data to generate accurate alerts and enable faster incident response.

