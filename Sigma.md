# Sigma

## 1. What is Sigma?
Sigma is a **generic detection rule format** used in Security Operations Centers (SOC) to describe suspicious behavior in logs. It is **SIEM-agnostic**, meaning it is not tied to any single SIEM product like Splunk, Sentinel, or QRadar.

Important points:
- Sigma does **not execute** on logs
- Sigma is **not a SIEM**
- Sigma defines **what to detect**, not **how to run it**

Sigma rules are later converted into a SIEM’s native query language.

---

## 2. Why SOCs use Sigma
SOCs use Sigma because:
- One rule can work across multiple SIEM platforms
- Detection logic is standardized
- Easier rule sharing and collaboration
- Vendor lock-in is reduced

Sigma helps SOC teams focus on **detection logic**, not tool syntax.

---

## 3. Core Components of a Sigma Rule

A typical Sigma rule contains:

- **title** – Name of the detection
- **description** – What the rule detects
- **logsource** – Type of logs required
- **detection** – Matching logic
- **condition** – When the rule should trigger
- **level** – Alert severity

Sigma rules work on **parsed and normalized events**, not raw log files.

---

## 4. Meaning of logsource in Sigma

`logsource` specifies the **logical source of logs**, not file paths.

Example meaning:
- product: windows → Windows operating system
- service: security → Security Event logs

Sigma does not read `.evtx` files. The SIEM already ingests and parses the logs before Sigma logic is applied.

---

## 5. Detection and Condition Logic

- **selection** defines what fields and values to look for
- **condition** tells Sigma which selection(s) must be true

Common condition types:
- Single event detection
- Threshold-based detection
- Multi-selection correlation

Sigma supports both **signature-based** and **behavior-based** detections.

---

## 6. SOC Flow of Sigma Rules

### Step 1: Log Generation
- Endpoints, servers, firewalls, applications generate logs

### Step 2: Log Collection
- Agents, syslog, or APIs send logs to the SIEM

### Step 3: Log Parsing and Normalization
- SIEM extracts fields (user, IP, process, event ID)

### Step 4: Sigma Rule Creation
- SOC analyst writes detection logic in Sigma format

### Step 5: Rule Conversion
- Sigma rule is converted to SIEM-native language
  - Splunk → SPL
  - Sentinel → KQL
  - QRadar → AQL

### Step 6: Rule Execution
- SIEM runs the converted rule on stored logs

### Step 7: Alert Generation
- If condition is met, alert is created

### Step 8: Investigation and Response
- Analyst investigates
- SOAR or EDR may take action

---

## 7. Sigma in Relation to Other SOC Tools

- **SIEM** – Executes converted Sigma rules on logs
- **EDR/XDR** – Generates telemetry that SIEM consumes
- **SOAR** – Uses Sigma-based alerts for automated response

Sigma sits at the **detection layer**, not the response layer.

---

## 8. Sigma Rule Lifecycle in SOC

Create → Convert → Test → Enable
→ Monitor → Tune → Review → Update or Retire

Sigma rules are **living detections**, continuously improved over time.

---

## 9. Key Takeaways

- Sigma is a **detection rule standard**, not a tool
- It works on **normalized SIEM data**, not log files
- Same Sigma rule can be reused across multiple SIEMs
- Sigma improves detection consistency in SOC environments

---

## Interview-ready Summary

Sigma provides a standardized way to define detection logic in SOCs, allowing security teams to write reusable, SIEM-independent rules that are converted and executed by SIEM platforms on ingested log data.

