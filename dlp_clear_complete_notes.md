# Data Loss Prevention (DLP) – Clear & Complete Notes

These notes summarize **everything discussed about DLP**, written in a **clean, logical, and interview‑ready** way.

---

## 1. What is DLP?

**Data Loss Prevention (DLP)** is a cybersecurity solution designed to **detect, monitor, and prevent unauthorized leakage of sensitive data**.

DLP protects data when it is:
- **At rest** (stored)
- **In use** (being accessed or copied)
- **In motion** (moving across network, email, cloud)

---

## 2. Why DLP is Needed

### 2.1 Common Ways Data Leaks Happen (Very Important)

Data leakage can occur **intentionally or accidentally** through many channels. Understanding these paths is critical to designing effective DLP.

#### A. Endpoint-Based Data Leaks
- Copying files to **USB / external hard drives**
- Copy–paste sensitive text into other files or apps
- Printing confidential documents
- Taking screenshots or screen recordings
- Saving files to personal folders or personal cloud sync

#### B. Email-Based Data Leaks (Most Common)
- Sending sensitive attachments to personal email
- Forwarding internal emails outside the organization
- Accidentally selecting wrong recipient
- CC / BCC misuse

#### C. Network & Internet-Based Leaks
- Uploading files to cloud storage (Google Drive, Dropbox)
- Web-based file sharing sites
- FTP / SCP transfers
- Messaging platforms (WhatsApp Web, Telegram Web)

#### D. Cloud & SaaS Data Leaks
- Publicly shared cloud links
- Misconfigured permissions
- Syncing work files to personal cloud accounts

#### E. Insider Threats
- Malicious employees stealing data
- Careless users violating policy
- Ex-employees retaining access

#### F. Malware & External Attacks
- Malware exfiltrating data
- Keyloggers stealing credentials
- Command-and-control data leaks

#### G. Physical & Human-Based Leaks (Hardest to Stop)
- Photos taken from screen using mobile phone
- Manual retyping of sensitive information
- Verbal disclosure

> **DLP is designed to reduce risk across digital channels, but human-based leaks require additional controls and awareness.**

---



Traditional security tools (Firewall, Antivirus) **do not understand data sensitivity**.

Common data‑leak scenarios:
- Copying files to USB
- Sending sensitive files via email
- Uploading data to cloud storage
- Insider threats (intentional or accidental)
- Malware stealing confidential information

**DLP focuses on the data itself, not just the action.**

---

## 3. Types of DLP

### 3.1 Endpoint DLP (E‑DLP)

Monitors **user devices** (PCs, laptops).

Controls:
- File copy / move
- USB & external storage
- Clipboard (copy‑paste)
- Printing
- Screen capture

Focus: **Data in use**

---

### 3.2 Network DLP (N‑DLP)

Monitors **data leaving the organization**.

Channels:
- Web uploads
- FTP / SCP
- Messaging apps
- Cloud traffic

Focus: **Data in motion**

---

### 3.3 Email / Cloud DLP

Specialized DLP for:
- Email body & attachments
- SaaS apps (Google Drive, OneDrive)

Focus: **Most common data‑leak channel**

---

## 4. How DLP Detects Sensitive Data

DLP does **content inspection**, not just file name or hash checks.

### 4.1 Regex (Pattern Matching)

Used for **structured data**:
- PAN numbers
- Aadhaar numbers
- Credit cards

Uses:
- Format patterns
- Checksum validation
- Context keywords

---

### 4.2 Keyword Matching

Detects **contextual sensitivity**.

Examples:
- Confidential
- FIR
- Investigation Report
- Internal Use Only

Modern DLP uses **multiple keywords + context** to avoid false positives.

---

### 4.3 Classification Labels

Files are tagged as:
- Public
- Internal
- Confidential
- Secret

Labels can be:
- Manually applied
- Automatically applied

Policies are enforced based on label.

---

### 4.4 Document Fingerprinting (Most Powerful)

Used to detect **specific sensitive documents**, even if:
- File name changes
- Format changes
- Only partial content is copied

---

## 5. How Document Fingerprinting Works

### Step 1: Content Extraction
- Text is extracted from files (DOC, PDF, ZIP, Email)

### Step 2: Normalization
- Remove formatting, case, extra spaces

### Step 3: Chunking (Sliding Window)

Example text:

"This is a confidential police investigation report"

Chunks:
- this is a confidential
- is a confidential police
- a confidential police investigation
- confidential police investigation report

---

### Step 4: Fingerprint Creation

Each chunk is converted into a **similarity‑preserving fingerprint**, not SHA‑256 or MD5.

Used techniques:
- Rolling hash
- Fuzzy hashing
- N‑grams
- SimHash‑like feature hashing

---

### Step 5: Fingerprint Storage

- Stored in **central DLP fingerprint database**
- Encrypted and non‑reversible
- Only signatures are stored, not full content

---

### Step 6: Matching & Similarity Scoring

When new data appears:
- Data is chunked again
- Fingerprints are compared
- Similarity score is calculated

If score ≥ policy threshold → **DLP action triggered**

---

## 6. Why Full Hash (SHA‑256 / MD5) Is NOT Used

| Reason | Explanation |
|----|----|
| Copy does not change original | Hash stays same |
| Partial copy | Hash fails |
| Format change | Hash fails |
| Email / clipboard data | No full file to hash |

**Hash is for integrity, not leakage detection.**

---

## 7. Where Fingerprints Are Used

### Endpoint DLP
- Local fingerprint cache
- Real‑time enforcement
- Works offline

### Network / Email DLP
- Traffic inspection
- Attachment & content scanning

Fingerprints are **distributed from central DLP server**.

---

## 8. What DLP Actually Monitors

DLP monitors **controlled channels**, not entire network blindly:
- File system events
- Email gateways
- Web proxies
- Cloud APIs

---

## 9. What DLP Does When Data Is Detected

Based on policy:
- Block
- Warn user
- Encrypt data
- Allow but log
- Alert SOC / SIEM

---

## 10. Limitations of DLP (Reality)

DLP cannot fully stop:
- Screenshots / photos
- Manual retyping
- Heavy paraphrasing
- Insider intent

So:
> **DLP reduces risk, it does not guarantee zero leakage**

---

## 11. One‑Line Interview Answer

**DLP is a distributed security system that monitors endpoints, networks, and cloud channels to inspect sensitive data using patterns, fingerprints, and labels, and prevents unauthorized data leakage in real time.**

---

## 12. Final Mental Model

- IAM → Who can access data
- DLP → Where data can go
- DRM → What can be done with data

All are required together.

---

✅ End of DLP Notes

