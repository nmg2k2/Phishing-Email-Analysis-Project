# 🎣 Phishing-Email-Analysis

> *Phishing is a type of cyberattack that uses fraudulent emails, text messages, phone calls, or websites to trick people into sharing sensitive data, downloading malware, or otherwise exposing themselves to cybercrime.*

## 🪐 Contents
* [Useful Tools](#useful-tools)
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

## 🛠️ Useful Tools

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
* **File:** [`phishing_sample.eml`](./phishing_sample.eml) *(Note: Ensure you upload your .eml file to the main folder of your repo so this link works!)*

---

## ✉️ Email Header
It is a section of an email that contains information like sender, recipient, date, and subject.

### Example:
```text
Date: Sun, 30 Jul 2023 23:57:35 +0000
To: phishing@pot
From: Binance <noreply-supportbinancewallet.irs@auswestbc.com.au>
Subject: [Binance] Withdraw Successful - 2023-07-30 51:51:51(UTC)
