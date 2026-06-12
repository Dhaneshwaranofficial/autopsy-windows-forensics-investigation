# Comprehensive Digital Forensic Analysis of a Compromised Windows System

![Autopsy](https://img.shields.io/badge/Autopsy-Forensics-blue?style=for-the-badge)
![Incident Response](https://img.shields.io/badge/Incident_Response-BEC_Investigation-red?style=for-the-badge)
![Windows XP](https://img.shields.io/badge/Environment-Windows_Endpoint-lightgrey?style=for-the-badge)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/dhaneshwaranofficial/)

## 📖 Project Overview
This project documents a digital forensic investigation conducted on a compromised corporate Windows disk image (M57-Jean scenario). The objective of this analysis was to identify indicators of compromise (IOCs), reconstruct user activity, and determine the exact exfiltration vector of highly sensitive corporate data (employee salaries and SSNs).

### 📝 Dataset Acknowledgement
This investigation utilizes the **M57-Jean** dataset provided by Digital Corpora. While the scenario is simulated, the analysis, methodology, and artifact extraction were conducted independently as a demonstration of applied digital forensics.

## 🛠️ Tools & Environment
* **Forensic Analysis Tool:** Autopsy (v4.23.1)
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

<p align="center">
  <img src="https://github.com/user-attachments/assets/1a46afe7-f966-4b65-948a-7fb56efb03d3" />
  <br>
  <i>Figure 1.1: Raw SMTP headers revealing the external origin of the spoofed email.</i>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/787e5c17-ac87-45b0-ab96-92d3af2047ce" />
  <br>
  <i>Figure 1.2: The initial grooming email spoofing the internal executive.</i>
</p>

### 2. Data Compilation
Falling for the social engineering lure, the user compiled the requested sensitive data into an Excel spreadsheet. 

* **Artifact Found:** Excel Spreadsheet (`m57biz.xls`)
* **Path:** `Documents and Settings/Jean/Desktop/m57biz.xls`
* **File Metadata:** The file was created on July 20, 2008 at 06:58:03 IST, perfectly aligning with the timeline immediately following the spoofed email request.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a6fc1c9c-6e5d-4641-b7a0-5ea5e3c3417f" />
  <br>
  <i>Figure 2: File metadata confirming the exact creation time of the exfiltrated spreadsheet.</i>
</p>

### 3. Data Exfiltration via Spear Phishing 
Shortly after the file was created, the attacker sent a second, high-urgency email demanding the data immediately. 

* **Artifact Found:** E-Mail Message (Phishing Payload / Exfiltration)
* **Timestamp:** July 20, 2008 06:58:00 IST (Reply)
* **Observation:** The user replied to the second urgent email, attaching the newly created `m57biz.xls` spreadsheet. The attacker utilized a deceptive `mailto:` reply address, routing the exfiltrated data directly to `tuckgorge@gmail.com`, inadvertently exposing corporate data to an unauthorized third party.

<p align="center">
  <img src="https://github.com/user-attachments/assets/de67daec-c347-441f-bbea-f0e8d9d5264d" />
  <br>
  <i>Figure 3: The targeted phishing email utilized to exfiltrate the data.</i>
</p>

---

## 📋 Insider Threat Assessment
* **Objective:** Determine if other internal employees were involved in the data exfiltration.
* **Methodology:** Conducted a comprehensive review of all internal communications (`@m57.biz`), raw SMTP headers of the exfiltration email, and system access logs via the Communications Visualization module.
* **Findings:** The communication regarding the sensitive data was strictly isolated between the victim and the external threat actor. 
* **Conclusion:** No other internal employees were involved. The incident was exclusively an external BEC attack, and the user was an unwitting victim of social engineering.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5f1ebe9f-a689-483d-83f6-9c9b27293aa1" />
  <br>
  <i>Figure 4: Communications Visualization timeline isolating the threat actor.</i>
</p>

---

## 💡 Conclusion & Remediation
The forensic analysis confirms that the corporate endpoint was not compromised via malware, but through a highly targeted social engineering campaign. The attacker successfully spoofed internal executive communications to extract a spreadsheet containing PII. 

**Modern Mitigation Strategy:** In a modern infrastructure environment, this specific attack lifecycle would be broken by implementing strict **SPF, DKIM, and DMARC** policies to prevent external servers from successfully spoofing the internal domain, alongside enforcing External Sender Warnings on the email client.

---
### 📬 Let's Connect
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/dhaneshwaranofficial/)
