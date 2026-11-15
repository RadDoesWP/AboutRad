
# Phishing Email Analysis: "Wildsino Casino Rewards"

**Tools used:** MX Toolbox, VirusTotal
**Verdict:** Spam / suspected phishing (malicious or unsolicited)

> All indicators below are **defanged** (`.` written as `[.]`, `@` as `[at]`) so they are not clickable or accidentally visited.

---

## Table of Contents

1. [Summary](#1-summary)
2. [Email Information](#2-email-information)
3. [Indicators of Compromise (IOCs)](#3-indicators-of-compromise-iocs)
4. [Analysis](#4-analysis)
   - [Email Header Analysis (MX Toolbox)](#41-email-header-analysis-mx-toolbox)
   - [Domain Reputation (VirusTotal)](#42-domain-reputation-virustotal)
5. [Threat Assessment](#5-threat-assessment)
6. [Recommended Security Actions](#6-recommended-security-actions)
7. [Conclusion](#7-conclusion)

---

## 1. Summary

On **16 April 2026**, an email titled **"Exclusive Offer Inside: 100 Free Spins for New Players at Wildsino bonus!"** was delivered to the monitored mailbox. The message impersonates a casino rewards promotion. Header analysis and domain reputation checks were performed to determine whether the email was malicious.

## 2. Email Information

| Field | Value |
|---|---|
| Sender display name | Wildsino casino rewards |
| Sender address | `Plinko[at]iceonearena[.]com` |
| Recipient | `phishing@pot` (truncated) |
| Date | 4/16/2026, 9:23 AM |
| Subject | Exclusive Offer Inside: 100 Free Spins for New Players at Wildsino bonus! |
| Sender IP | `172[.]104[.]186[.]169` (Akamai Connected Cloud / Linode) |

<!-- Add a screenshot of the email here (blur anything sensitive) -->
![Email overview](images/email-overview.png)

## 3. Indicators of Compromise (IOCs)

| Type | Indicator | Context |
|---|---|---|
| Email address | `Plinko[at]iceonearena[.]com` | Sender address |
| Domain | `iceonearena[.]com` | Sender domain, does not match the "Wildsino" brand |
| IP address | `172[.]104[.]186[.]169` | Sending IP (Akamai Connected Cloud / Linode) |
| Domain | `woondsplay[.]com` | Flagged as malicious on VirusTotal (8/92 vendors) |

## 4. Analysis

### 4.1 Email Header Analysis (MX Toolbox)

<img width="1482" height="719" alt="image" src="https://github.com/user-attachments/assets/783467fd-0ceb-4605-bccd-77a9c5be0d10" />
<img width="1494" height="688" alt="image" src="https://github.com/user-attachments/assets/bf9f4dae-199d-4b53-82ec-93522a2d11fd" />
<img width="1485" height="574" alt="image" src="https://github.com/user-attachments/assets/8dbc2c7c-370e-4154-9e7c-337278d5e161" />

| Check | Result |
|---|---|
| **Sender** | `Plinko[at]iceonearena[.]com`, impersonates a casino rewards promotion offering 100 free spins |
| **Authentication** | SPF, DKIM and DMARC passed per Microsoft's `Authentication-Results` header, although the DKIM alignment check shows an inconsistency |
| **DMARC policy** | `p=none`, so failed authentication does not trigger quarantine or rejection |
| **Sending IP** | `172[.]104[.]186[.]169`, originating from `iceonearena[.]com`; not listed on the reported blacklist checks |
| **Spam score** | Microsoft assigned an **SCL of 8**, indicating a high likelihood of spam |

**Takeaway:** The gambling promotion, authentication inconsistencies and high spam score warrant treating this email as malicious or unsolicited. Passing SPF/DKIM/DMARC only proves the sender controls the domain, not that the email is legitimate.

### 4.2 Domain Reputation (VirusTotal)

<img width="1537" height="669" alt="image" src="https://github.com/user-attachments/assets/0e1d8a51-3d97-4d48-a195-18317998a892" />
<img width="974" height="803" alt="image" src="https://github.com/user-attachments/assets/bd4e8903-cf30-4798-88b6-d9960b782895" />

**Points of concern**

- **Recently registered:** A relatively young domain has less established reputation and history.
- **Phishing classifications:** Fortinet and alphaMountain.ai independently identify phishing activity.
- **Malware classification:** VIPRE flags the domain for malware.
- **Multiple malicious verdicts:** Bkav, CRDF, Seclookup, SOCRadar and Webroot also flag it.
- **Mixed reputation:** Google Safe Browsing and several other established vendors show clean results. This is not proof of legitimacy.

## 5. Threat Assessment

| Threat category | Assessment |
|---|---|
| Phishing | Elevated concern |
| Malware distribution | Elevated concern |
| Spam / unwanted activity | Flagged |
| Credential theft | Possible, unconfirmed |
| Drive-by downloads | Unconfirmed |
| Confirmed compromise | Not established |

## 6. Recommended Security Actions

1. Block `woondsplay[.]com` at the DNS, web proxy and endpoint security layers as a precaution.
2. Search DNS, proxy, firewall and endpoint logs for connections to the domain.
3. Identify the source device, user, timestamp and URL path associated with any connection.
4. If a user entered credentials on the site, reset affected credentials and revoke active sessions.
5. If files were downloaded, investigate them in an isolated malware-analysis environment.
6. Preserve relevant logs and timestamps for incident investigation.

## 7. Conclusion

The domain `woondsplay[.]com` was identified as suspicious based on VirusTotal reputation analysis, with **8 out of 92** security vendors flagging it for malicious activity. Detections include phishing, malware, spam and general malicious classifications.

Although several vendors report the domain as clean, the number and consistency of malicious verdicts indicate a potential security threat. The domain should be treated as suspicious, blocked as a precaution, and investigated for possible connections within the organization's network. Further analysis is required to establish whether any successful compromise or credential exposure occurred.

---

*Report created for educational and portfolio purposes.*
