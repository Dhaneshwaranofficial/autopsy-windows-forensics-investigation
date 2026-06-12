# Comprehensive Digital Forensic Analysis of a Compromised Windows System

![Autopsy](https://img.shields.io/badge/Autopsy-Forensics-blue)
![Incident Response](https://img.shields.io/badge/Incident_Response-BEC_Investigation-red)
![Windows XP](https://img.shields.io/badge/Environment-Windows_Endpoint-lightgrey)

## 📖 Project Overview
This project documents a digital forensic investigation conducted on a compromised corporate Windows disk image (M57-Jean scenario). The objective of this analysis was to identify indicators of compromise (IOCs), reconstruct user activity, and determine the exact exfiltration vector of highly sensitive corporate data (employee salaries and SSNs).

### 📝 Dataset Acknowledgement
This investigation utilizes the **M57-Jean** dataset provided by Digital Corpora. While the scenario is simulated, the analysis, methodology, and artifact extraction were conducted independently as a demonstration of applied digital forensics.

## 🛠️ Tools & Environment
* **Forensic Analysis Tool:** Autopsy (v4.x)
* **Target OS Environment:** Windows XP (Corporate Endpoint)
* **Core Modules Run:** Recent Activity, Keyword Search, Email Parser, Extension Mismatch Detector

---

## 🔍 Evidence Acquisition & Preparation
To maintain the integrity of the investigation, the evidence was verified upon ingestion into Autopsy.
* **Image File:** `nps-2008-jean.E01`
* **Acquisition Format:** EnCase Image Format (E01)

---

## 🔬 Analysis & Key Findings

### 1. The Lure: Social Engineering & Grooming
The investigation revealed a multi-stage Business Email Compromise (BEC) attack. The threat actor initiated contact by spoofing an internal executive's email address to establish authority and request the compilation of sensitive data under the guise of an investor background check.

* **Artifact Found:** E-Mail Message (Initial Request)
* **Timestamp:** July 20, 2008 05:09:57 IST
* **Forensic Evidence:** While the display name read `alison@m57.biz`, analysis of the raw SMTP headers revealed a `Return-Path` of `<simsong@xy.dreamhostps.com>` and an originating server of `smarty.dreamhost.com`. This proves the email bypassed internal corporate routing and originated from an external host. 

*image of the email header and luring the CFO like the real boss <img width="1919" height="1027" alt="email-header" src="https://github.com/user-attachments/assets/a6dba497-03a9-425c-bf78-dfc36d439c30" /> and <img width="1919" height="1027" alt="Luring jean like a real boss" src="https://github.com/user-attachments/assets/df1189d9-df06-499f-b597-9f1b48f716bf" />*

### 2. Data Compilation
Falling for the social engineering lure, the user compiled the requested sensitive data into an Excel spreadsheet. 

* **Artifact Found:** Excel Spreadsheet (`m57biz.xls`)
* **Path:** `Documents and Settings/Jean/Desktop/m57biz.xls`
* **File Metadata:** The file was created on July 20, 2008 at 06:58:03 IST, perfectly aligning with the timeline immediately following the spoofed email request.

* File created from Jeans computer <img width="1711" height="918" alt="File created from Jeans computer" src="https://github.com/user-attachments/assets/42cc40a5-929f-4fd7-be72-b47bde8af07d" />*

### 3. Data Exfiltration via Spear Phishing 
Shortly after the file was created, the attacker sent a second, high-urgency email demanding the data immediately. 

* **Artifact Found:** E-Mail Message (Phishing Payload / Exfiltration)
* **Timestamp:** July 20, 2008 05:14:00 IST (Reply)
* **Observation:** The user replied to the second urgent email, attaching the newly created `m57biz.xls` spreadsheet. The attacker utilized a deceptive `mailto:` reply address, routing the exfiltrated data directly to `tuckgorge@gmail.com`, inadvertently exposing corporate data to an unauthorized third party.

* Jean got phished = <img width="1917" height="1034" alt="Jean got phished" src="https://github.com/user-attachments/assets/3745d47d-c652-444d-9cf4-ddfa2f3019de" />*

---

## 📋 Insider Threat Assessment
* **Objective:** Determine if other internal employees were involved in the data exfiltration.
* **Methodology:** Conducted a comprehensive review of all internal communications (`@m57.biz`), raw SMTP headers of the exfiltration email, and system access logs via the Communications Visualization module.
* **Findings:** The communication regarding the sensitive data was strictly isolated between the victim and the external threat actor. 
* **Conclusion:** No other internal employees were involved. The incident was exclusively an external BEC attack, and the user was an unwitting victim of social engineering.

<p align="center">
  <img src="[<img width="1917" height="1027" alt="Communications" src="https://github.com/user-attachments/assets/5f1ebe9f-a689-483d-83f6-9c9b27293aa1" />]" alt="Communications Visualization">
  <br>
  <i>Figure 4: Communications Visualization timeline isolating the threat actor.</i>
</p>

---

## 💡 Conclusion & Remediation
The forensic analysis confirms that the corporate endpoint was not compromised via malware, but through a highly targeted social engineering campaign. The attacker successfully spoofed internal executive communications to extract a spreadsheet containing PII. 

**Modern Mitigation Strategy:** In a modern infrastructure environment, this specific attack lifecycle would be broken by implementing strict **SPF, DKIM, and DMARC** policies to prevent external servers from successfully spoofing the internal domain, alongside enforcing External Sender Warnings on the email client.

```
---
### 📬 Let's Connect
* **LinkedIn:** [https://www.linkedin.com/in/dhaneshwaranofficial/]
