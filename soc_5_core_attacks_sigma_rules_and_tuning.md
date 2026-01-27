# SOC Practical Playbook: 5 Common Attacks with Sigma Rules & Tuning

This document shows **5 very common SOC attacks**, each with:
- What the attack is
- A **Sigma rule** (example)
- Why it triggers
- **False positives**
- **How to tune it in real SOC**

These are **learning-grade but realistic** rules.

---

## 1️⃣ SSH Brute Force Attack (Linux)

### Attack idea
Attacker tries many passwords over SSH to gain access.

---
### Sigma Rule
```yaml
title: SSH Brute Force Attempt
id: 1001-ssh-bruteforce
status: experimental
description: Detects multiple failed SSH login attempts
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
### Why this works
- SSH logs record `Failed password`
- Repeated failures indicate brute force

---
### False Positives
- Admin mistyping passwords
- Vulnerability scanners

---
### SOC Tuning
- Add **thresholding in SIEM** (e.g. 5+ attempts in 5 minutes)
- Exclude trusted admin IPs

---

## 2️⃣ Web Directory / File Scanning

### Attack idea
Attacker scans common URLs like `/admin`, `/login.php`, `/phpmyadmin`.

---
### Sigma Rule
```yaml
title: Web Directory Scanning
id: 1002-web-scan
status: experimental
description: Detects scanning of sensitive web paths
author: rizwan
logsource:
  category: webserver

detection:
  selection:
    cs-uri-stem|contains:
      - "/admin"
      - "/login"
      - "/phpmyadmin"
  condition: selection

level: medium
```

---
### Why this works
- Attackers probe common admin paths

---
### False Positives
- Security testing
- Internal QA testing

---
### SOC Tuning
- Alert only if **multiple different paths** requested by same IP
- Exclude company IP ranges

---

## 3️⃣ Log Deletion / Covering Tracks (Linux)

### Attack idea
After compromise, attacker deletes logs to hide evidence.

---
### Sigma Rule
```yaml
title: Log File Deletion Attempt
id: 1003-log-delete
status: experimental
description: Detects deletion of log files using rm or shred
author: rizwan
logsource:
  product: linux

detection:
  selection:
    Image|endswith:
      - "/rm"
      - "/shred"
    CommandLine|contains:
      - "/var/log"
      - "/var/spool/mail"
  condition: selection

level: high
```

---
### Why this works
- `rm` or `shred` targeting logs is suspicious

---
### False Positives
- Log rotation scripts
- Cleanup cron jobs

---
### SOC Tuning
- Exclude known logrotate processes
- Alert only when executed by **non-root service accounts**

---

## 4️⃣ Suspicious File Transfer (Data Exfiltration)

### Attack idea
Attacker copies files out using `scp`, `rsync`, or `sftp`.

---
### Sigma Rule
```yaml
title: Suspicious File Transfer Tools Usage
id: 1004-data-exfil
status: experimental
description: Detects possible data exfiltration via SCP, RSYNC, or SFTP
author: rizwan
logsource:
  product: linux

detection:
  tools:
    - "scp"
    - "rsync"
    - "sftp"
  remote_indicator:
    - "@"
    - ":"
  condition: tools and remote_indicator

level: high
```

---
### Why this works
- Remote copy commands usually contain `user@host:/path`

---
### False Positives
- Admin file transfers
- Backup jobs

---
### SOC Tuning
- Whitelist backup servers
- Alert only for **large file transfers** or **off-hours**

---

## 5️⃣ Windows Persistence via Registry (Active Setup)

### Attack idea
Malware uses registry persistence to execute on every login.

---
### Sigma Rule
```yaml
title: Active Setup Persistence Registry Modification
id: 1005-active-setup
status: experimental
description: Detects persistence via Active Setup StubPath
author: rizwan
logsource:
  product: windows
  category: registry_event

detection:
  selection:
    TargetObject|startswith: "HKLM\\SOFTWARE\\Microsoft\\Active Setup\\Installed Components"
    TargetObject|endswith: "\\StubPath"
  filter_chrome:
    Details|contains: "Chrome"
  filter_edge:
    Details|contains: "Edge"
  condition: selection and not 1 of filter_*

level: high
```

---
### Why this works
- Active Setup is a known persistence method

---
### False Positives
- Browser installers
- Legitimate software updates

---
### SOC Tuning
- Whitelist known installer processes
- Alert only if created by **unknown binaries**

---

## 🧠 Final SOC Mindset

- Sigma rules **define detection logic**
- SIEM **executes and alerts**
- Analysts **tune and validate**

> Good detection = signal + tuning + context

---

## ✅ How to Practice
1. Pick one rule
2. Take real logs
3. Manually test the logic (`grep`, `awk`)
4. Convert rule to SIEM
5. Tune false positives

---

**You now have a mini SOC detection playbook.**

