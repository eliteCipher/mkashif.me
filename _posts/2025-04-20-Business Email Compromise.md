---
title: "Business Email Compromise: Emotet"
tags: [Cybersecurity, BEC, Emotet]
style:
color:
image: "/assets/images/post_7/bec.jpg"
description: "Discussing Emotet, Initially designed as a banking trojen, this malware is now being used as a landing platform for other malware."
permalink: Business-Email-Compromise
---

{% include elements/figure.html image="/assets/images/post_7/bec.jpg" caption='Business Email Compromise' %}

# 🚨 Business Email Compromise 🚨 

Sounds threatening?

It should!	

It is one of the most trending threat models in today’s cyber landscape. BEC attacks email systems by mostly leveraging phishing techniques to steal sensitive information and facilitate financial fraud.
While talking about BEC, the very first thing that came to my mind is Emotet. Initially designed as a banking trojen, this malware is now being used as a landing platform for other malware.

Let's break down the Emotet's mechanism to understand the threat it poses:
#### 1. Account Manipulation

- Bruteforcing Credentials: Attackers try multiple logon attempts (Event ID 4625) to crack user credentials.
- Account Changes: Look for account modification events (Event IDs 4781 and 4738) indicating potential manipulation (MITRE T1098).
- Credential Dumping: Tools like Mimikatz or ProcDump are used—or Sysmon Event ID 10 (targeting lsass.exe) is logged—to steal credentials (MITRE T1003.001).

#### 2. Email Manipulation

- Sending Emails: Compromised accounts are used to send malicious emails, spreading the infection.
- Email Collection: Attackers harvest email data (MITRE T1114-1 for further exploitation.
- Delegate Permission Changes: Unauthorized changes to email delegate permissions (MITRE T1098.002) are made to control email flow.

#### 3. Installing Other Malware

Emotet downloads and executes additional malware, such as ransomware or banking Trojans, extending its reach and impact.

Some BEC related threat detection techniques are on my <a target="_blank" href="https://github.com/eliteCipher/Threat-Detection/tree/main/BEC">git repository</a> for your reference.

