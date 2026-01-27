# YARA

## 1. What is YARA?
YARA is a **pattern-matching rule language** used to **identify and classify malware** based on file content, memory patterns, or strings.

Unlike Sigma:
- YARA works on **files and memory**, not logs
- YARA performs **direct inspection**
- YARA is commonly used in **malware analysis and endpoint detection**

In SOC terms, YARA answers:
> “Does this file or memory look like known malware?”

---

## 2. Why SOCs use YARA

SOCs use YARA because:
- It detects **known malware families**
- It works even when filenames change
- It can scan files, memory, and disk
- It is widely supported by EDR and sandbox tools

YARA is very effective for **signature-based malware detection**.

---

## 3. Core Components of a YARA Rule

A YARA rule typically contains:

- **rule name** – Identifier of the rule
- **meta** – Information about the rule
- **strings** – Patterns to match
- **condition** – Logic to trigger a match

YARA rules directly analyze **binary content**, not parsed events.

---

## 4. What YARA Works On

YARA can scan:
- Files on disk
- Email attachments
- Memory processes
- Malware samples in sandboxes

YARA does **not** scan logs and does **not** depend on log sources.

---

## 5. Detection and Condition Logic in YARA

- **strings** define malware indicators
- **condition** defines how many indicators must match

Detection can be:
- Single string match
- Multiple string match
- Combination of strings and file properties

YARA focuses on **content-based detection**.

---

## 6. SOC Flow of YARA Rules

### Step 1: File or Memory Creation
- File downloaded
- Email attachment received
- Process loaded into memory

### Step 2: YARA Scan Execution
- Endpoint agent, sandbox, or analysis tool runs YARA

### Step 3: Pattern Matching
- YARA scans file or memory against rules

### Step 4: Match Detection
- Rule condition is satisfied
- Malware match is identified

### Step 5: Alert or Action
- EDR blocks or quarantines file
- Detection log is generated

### Step 6: Log Forwarding to SIEM
- YARA match results are sent to SIEM

### Step 7: SOC Investigation
- Analyst reviews detection
- Correlation with other alerts

---

## 7. YARA in Relation to Other SOC Tools

- **EDR/XDR** – Executes YARA scans
- **Sandbox** – Uses YARA during malware detonation
- **SIEM** – Receives YARA detection logs
- **SOAR** – Automates response actions

YARA sits at the **malware detection layer**, not the correlation layer.

---

## 8. YARA Rule Lifecycle in SOC

Create → Test → Deploy
→ Detect → Alert → Investigate
→ Update or Retire

YARA rules must be updated as malware evolves.

---

## 9. Sigma vs YARA (SOC View)

| Aspect | Sigma | YARA |
|-----|------|------|
| Detects | Attacker behavior | Malware content |
| Works on | Logs | Files / Memory |
| Runs in | SIEM | EDR / Sandbox |
| Output | Alerts | Malware match |

---

## 10. Key Takeaways

- YARA detects **what malware is**, not what attackers do
- It works directly on files and memory
- SIEM consumes YARA results, not raw scans
- YARA complements Sigma in SOC operations

---

## Interview-ready Summary

YARA is a powerful malware detection rule language used in SOCs to identify malicious files and memory artifacts through pattern matching, while SIEM platforms consume YARA detection results for correlation and response.

