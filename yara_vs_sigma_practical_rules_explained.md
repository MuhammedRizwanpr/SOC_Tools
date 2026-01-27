# One YARA Rule & One Sigma Rule — Line‑by‑Line Explanation

This file contains:
- **1 YARA rule** (file / log pattern matching)
- **1 Sigma rule** (log detection design)

Each rule is followed by a **line‑by‑line explanation** so you clearly see the difference and purpose.

---

## 🟣 PART 1: YARA Rule (IP Address Detection)

### YARA Rule
```yara
rule Detect_IPv4_Address
{
    meta:
        author = "rizwan"
        description = "Detects IPv4 addresses in files or logs"

    strings:
        $ip = /\b\d{1,3}(\.\d{1,3}){3}\b/

    condition:
        $ip
}
```

---

### 🔍 Line‑by‑Line Explanation (YARA)

```yara
rule Detect_IPv4_Address
```
• Name of the rule
• Used in output when a match is found

---

```yara
meta:
```
• Metadata section
• Only for humans (no effect on detection)

---

```yara
author = "rizwan"
```
• Who wrote the rule

---

```yara
description = "Detects IPv4 addresses in files or logs"
```
• What the rule is meant to detect

---

```yara
strings:
```
• Section where patterns are defined

---

```yara
$ip = /\b\d{1,3}(\.\d{1,3}){3}\b/
```
• `$ip` = string identifier
• Regex matches IPv4 pattern (X.X.X.X)
• `\b` = word boundary
• `{3}` repeats the dot+number group three times

---

```yara
condition:
```
• Logic section
• Defines when rule triggers

---

```yara
$ip
```
• Rule triggers if **any IPv4 address is found**

---

### 🧠 What this YARA rule does
> Scans a file or log and triggers if it finds any IPv4‑like address.

---

## 🔵 PART 2: Sigma Rule (SSH Failed Login Detection)

### Sigma Rule
```yaml
title: SSH Failed Login Attempt
id: 2001-ssh-failed-login
status: experimental
description: Detects failed SSH login attempts
author: rizwan

logsource:
  product: linux
  service: sshd

detection:
  selection:
    message|contains: "Failed password"
  condition: selection

level: medium
```

---

### 🔍 Line‑by‑Line Explanation (Sigma)

```yaml
title: SSH Failed Login Attempt
```
• Human‑readable rule name

---

```yaml
id: 2001-ssh-failed-login
```
• Unique identifier for the rule

---

```yaml
status: experimental
```
• Rule maturity (experimental / stable)

---

```yaml
description: Detects failed SSH login attempts
```
• What attack behavior this rule detects

---

```yaml
author: rizwan
```
• Rule creator

---

```yaml
logsource:
```
• Defines **where logs come from**

---

```yaml
product: linux
```
• Logs are from Linux OS

---

```yaml
service: sshd
```
• Logs are from SSH service

---

```yaml
detection:
```
• Detection logic section

---

```yaml
selection:
```
• A named matching block

---

```yaml
message|contains: "Failed password"
```
• Looks for this text inside log message
• `|contains` is a Sigma modifier (not OR)

---

```yaml
condition: selection
```
• Rule triggers if `selection` matches

---

```yaml
level: medium
```
• Alert severity level

---

### 🧠 What this Sigma rule does
> Describes a detection that alerts when SSH authentication failures appear in Linux SSH logs.

---

## 🔴 FINAL COMPARISON (VERY IMPORTANT)

| Feature | YARA | Sigma |
|------|------|------|
Scans logs/files directly | ✅ Yes | ❌ No |
Prints matches | ✅ Yes | ❌ No |
Used for malware | ✅ Yes | ❌ No |
Used for SOC detections | ⚠️ Limited | ✅ Yes |
Executed by | YARA engine | SIEM |

---

## 🔑 Final Takeaway

> **YARA finds patterns directly. Sigma defines detections that SIEM executes.**

You now have a **clear mental model** of both tools.

