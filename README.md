# 🎣 Phishing-Email-Analysis

> *Phishing is a type of cyberattack that uses fraudulent emails, text messages, phone calls, or websites to trick people into sharing sensitive data, downloading malware, or otherwise exposing themselves to cybercrime.*

## 🪐 Contents
* [Used Tools](#useful-tools)
* [Overview](#overview)
* [Sample Email File](#sample-email-file)
* [Email Header](#email-header)
  * [Example](#example)
* [Email Header Analysis](#email-header-analysis)
* [Authentication Analysis](#authentication-analysis)
* [Static Analysis](#static-analysis)
* [VirusTotal](#virustotal)
* [MITRE ATT&CK Mapping](#mitre-attck-mapping)
* [Risk Assessment & Recommendations](#risk-assessment--recommendations)

---

## 🛠️ Used Tools

**Email Header & Authentication Analysis**
* MXToolbox

**Reputation Check & URL Analysis**
* VirusTotal

**Threat Mapping**
* MITRE ATT&CK Framework

---

## 🔎 Overview
This project documents a Tier-1 SOC investigation into a suspected phishing email designed to steal cryptocurrency credentials. The investigation confirmed that the email is a highly deceptive phishing attempt leveraging Binance brand impersonation to panic the user into clicking a malicious link.

---

## 📁 Sample Email File
For hands-on analysis, the raw email file has been included in this repository. 

* ⚠️ **WARNING:** This is a real phishing sample containing malicious links. Handle with care and open only in a safe, sandboxed environment.
* **File:** [`phishing_sample.eml`](./sample-1007.eml)

---

## ✉️ Email Header
It is a section of an email that contains information like sender, recipient, date, and subject.

## ✉️ Email Header
It is a section of an email that contains information like sender, recipient, date, and subject.

### Example:
```text
Date: Sun, 30 Jul 2023 23:57:35 +0000
To: phishing@pot
From: Binance <noreply-supportbinancewallet.irs@auswestbc.com.au>
Subject: [Binance] Withdraw Successful - 2023-07-30 51:51:51(UTC)
📊 Email Header Analysis
When we suspect an email is phishing, we need to check the headings during a Phishing analysis:

Was the email sent from the correct SMTP server?

Are the data "From" and "Return-Path / Reply-To" the same?

In this example, the data is different. The display name shows as "Binance", but the actual From address is auswestbc.com.au. Furthermore, the originating IP address was identified as 69.169.224.12. A WHOIS lookup confirms this IP is associated with Amazon Web Services (AWS) infrastructure and has no relation to Binance. The return-path address is completely different from the actual from-address of the email.

🔐 Authentication Analysis
Using tools like MXToolbox to analyze the headers reveals the status of email authentication protocols:

SPF Result: Passed

DKIM Result: Passed

DMARC Result: No policy

Even though SPF and DKIM are passed, they are not aligned. This means the email sending server and DKIM signature are validating the spoofed domain (auswestbc.com.au), not the actual brand (Binance).

🛑 Static Analysis
Static analysis of a phishing email involves examining the e-mail without executing its contents. Analysts review other attributes such as sender information, email content, links, and attachments to identify potential signs of phishing. Attackers can use HTML to create emails that hide malicious URLs behind buttons or text that appear to be harmless.

As seen in this email, the address the user sees when clicking on a link can be different (the real address is seen when the user hovers over the link). The email contains a fake "Cancel Transaction" button. Hovering over it reveals the true malicious destination: https://shylshom.com/.

🦠 VirusTotal
By querying VirusTotal for web addresses in emails, you can find out if the antivirus engines detect the web address as harmful. If someone else has already analyzed the same address/file in VirusTotal, VirusTotal will not analyze it from scratch, it will show you the old analysis result.

Domain Check: The sender domain http://auswestbc.com.au/ was flagged by 5/95 security vendors as Malicious.

URL Check: The extracted payload URL https://shylshom.com/ was flagged by 6/95 security vendors (including ADMINUSLabs, CRDF, and G-Data) as Malicious/Phishing.

🗺️ MITRE ATT&CK Mapping
Tactic: Credential Access (TA0006)

Technique: T1566 - Phishing

Sub-technique: T1566.002 - Spearphishing Link

Description: The adversary utilized a deceptive email masquerading as a Binance withdrawal alert. The email contains a malicious link designed to direct the victim to a credential harvesting site under the guise of cancelling a fraudulent transaction.

⚠️ Risk Assessment & Recommendations
Risk Level: HIGH (Credential Theft & Brand Impersonation)

Actionable Recommendations:

Block the malicious domain at the email gateway.

Enable DMARC enforcement policies.

Use URL filtering and sandboxing.

Monitor email logs for similar patterns.

User Awareness: Utilize this email template in the next internal phishing simulation.
