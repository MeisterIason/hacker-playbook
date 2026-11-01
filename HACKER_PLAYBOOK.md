# Hacker Playbook — Authorized Offensive Security

> **Ethical use only.** This playbook is for authorized penetration testing, bug bounty programs with explicit scope, and defensive security research. Unauthorized access is illegal and unethical. Always obtain written permission before testing.

## 0. Mindset & Principles

1. **Scope is law.** If it's not in scope, it's off limits.
2. **Document everything.** Evidence, timestamps, commands, outputs.
3. **Minimize impact.** Do no harm to production data.
4. **Assume breach.** Think like an adversary, defend like an engineer.
5. **Continuous learning.** Exploit techniques evolve weekly.

## 1. Pre-Engagement

### 1.1 Legal & Administrative
- Signed Rules of Engagement RoE
- Scope definition: IP ranges, domains, subdomains, applications
- Out-of-scope systems, sensitive data handling
- Communication channels, escalation contacts
- Time windows, maintenance windows
- Reporting format and SLA

### 1.2 Reconnaissance Planning
- Passive first, active second
- Build target inventory
- Identify tech stack, cloud providers, SaaS
- Map critical assets

### 1.3 Tooling Setup
- Isolated lab / VPN
- Virtual machines: Kali, Parrot, custom
- Logging: all commands to `engagement.log`
- Credential vault, no secrets in repo
- Backup and restore plan

## 2. Reconnaissance

### 2.1 Passive Recon
**OSINT**
- WHOIS, RDAP
- DNS history: securitytrails, viewdns
- Certificate transparency logs
- Social media, LinkedIn, staff pages
- Code repositories, Pastebin, GitHub leaks
- Shodan, Censys, FOFA fingerprints

**Command examples**
```
whois target.com
dig axfr target.com @ns1
crt.sh "%target.com%"
```

### 2.2 Active Recon
- Subdomain enumeration: subfinder, amass, findomain
- Port scanning: nmap stealth
```
nmap -sS -sV -Pn -top-ports 1000 target
```
- Service versioning, banner grabbing
- DNS brute forcing with wordlists

### 2.3 Mapping
- Draw network map, attack surface
- Identify entry points: web, VPN, APIs, mobile
- Document findings in `recon.md`

## 3. Vulnerability Enumeration

### 3.1 Web Applications
- Tech fingerprint: WhatWeb, Wappalyzer
- Directory brute force: gobuster, ffuf
- Parameter discovery: arjun
- Common flaws: IDOR, SSRF, XSS, CSRF, Open Redirect, File Upload

### 3.2 Network Services
- SMB, RDP, SSH brute force with caution
- Vulnerable services from nmap scripts
- TLS misconfigurations, certificate checks

### 3.3 Cloud & Infrastructure
- S3 bucket enumeration
- Misconfigured DNS
- Exposed dashboards, Grafana, Jenkins

## 4. Exploitation Methodology

### 4.1 Exploitation Principles
- Verify vuln before exploit
- Use least privileged exploit
- Snapshot state before and after
- Chain vulnerabilities for higher impact

### 4.2 Web Exploitation Workflow
1. Confirm parameter injection
2. Build PoC with minimal payload
3. Escalate privilege if possible
4. Document steps

### 4.3 Post-Exploitation
- Stabilize shell
- Enumerate system: user, groups, processes
- Privilege escalation checks
- Lateral movement only within scope
- Data exfiltration simulation with dummy files

## 5. Privilege Escalation

### 5.1 Linux
- SUID binaries, cron jobs
- Kernel exploits, misconfigured sudo
- Cloud metadata access

### 5.2 Windows
- SeImpersonate, SeBackupPrivilege
- Scheduled tasks, WMI
- Token manipulation

## 6. Post-Exploitation & Persistence

Only for authorized red team scopes:
- Establish foothold, document
- Avoid persistence unless explicitly allowed
- Clean up artifacts

## 7. Reporting

### 7.1 Executive Summary
- Business risk, not technical jargon
- Impact, likelihood, remediation priority

### 7.2 Technical Findings
Each finding includes:
- Title, severity CVSS
- Description, steps to reproduce
- Evidence: screenshots, logs
- Impact
- Remediation
- References

### 7.3 Deliverables
- PDF report
- Raw evidence archive
- Re-implementation guide

## 8. Common Attack Chains

### 8.1 Supply Chain
Subdomain takeover → SSRF → internal API

### 8.2 Initial Access → Priv Escalation
Phishing → RDP → Kerberoasting → DCSync

### 8.3 Web to Network
XSS → Session hijack → Admin panel → SSH key download

## 9. Tool Arsenal

**Recon**: amass, subfinder, httpx, dnsx
**Scanning**: nmap, rustscan, masscan
**Web**: burpsuite, ffuf, nuclei, sqlmap
**Exploitation**: metasploit, custom scripts
**Forensics**: volatility, sleuthkit

## 10. Defensive Countermeasures

- Patch management
- WAF tuning
- MFA everywhere
- Network segmentation
- Logging and SIEM
- Regular pentests

## 11. Legal & Ethics Checklist

- [ ] Written permission obtained
- [ ] Scope clearly defined
- [ ] No personal data collection
- [ ] No denial of service
- [ ] Report delivered on time
- [ ] Secrets destroyed post-engagement

## 12. Continuous Improvement

- After-action review
- Update playbook with new techniques
- Track IOCs and TTPs
- Share knowledge internally

---

Appendix A: Wordlists, payloads, checklists
- Subdomain wordlists: SecLists
- Common directories: /admin, /backup, /config
- SQLi payloads: classic boolean, time-based
- XSS payloads: <svg onload=alert(1)>

Appendix B: Reporting templates
```
Finding ID: F-001
Title: ...
Severity: High
CVSS: 8.2
...
```

Appendix C: Legal references by jurisdiction
- US: CFAA 18 U.S.C. §1030
- EU: NIS2 Directive
- UK: Computer Misuse Act 1990

Appendix D: Daily Checklist
- [ ] Review scope
- [ ] Update recon notes
- [ ] Log all commands
- [ ] Take screenshots
- [ ] Verify impact

Appendix E: Red Team Rules
- No damage to production
- No data exfiltration beyond dummy
- Immediate stop on encountering safety triggers

## 13. Resources & References

### 13.1 Essential Tools
- **Recon**: amass, subfinder, findomain, httpx, dnsx, chaos, theHarvester
- **Scanning**: nmap, rustscan, masscan, naabu
- **Web**: Burp Suite, OWASP ZAP, ffuf, gobuster, nuclei, sqlmap, arjun
- **Exploitation**: Metasploit Framework, impacket, BloodHound
- **Forensics**: Volatility, Rekall, Sleuth Kit, Autopsy
- **Automation**: Python requests, go tooling, bash

### 13.2 GitHub Repos & Collections
- SecLists - https://github.com/danielmiessler/SecLists
- Awesome Hacking - https://github.com/carlospolop/awesome-hacking
- Awesome Bug Bounty - https://github.com/digininja/Awesome-Bug-Bounty
- Pentest-Tools - https://github.com/rapid7/metasploit-framework
- BloodHound - https://github.com/BloodHoundAD/BloodHound
- Nuclei Templates - https://github.com/projectdiscovery/nuclei-templates
- OSINT Framework - https://github.com/jivoi/OSINT-Framework

### 13.3 Wikis & Documentation
- OWASP Testing Guide - https://owasp.org/www-project-web-security-testing-guide/
- OWASP Cheat Sheets - https://cheatsheetseries.owasp.org/
- MITRE ATT&CK - https://attack.mitre.org/
- SANS Reading Room - https://www.sans.org/reading-room/
- HackTricks - https://book.hacktricks.xyz/

### 13.4 Forums & Communities
- Reddit r/NetSec, r/Pentesting, r/OSINT
- StackExchange Information Security
- Discord: Pentest Crew, HackTheBox Community
- Twitter/X Security Researchers
- Bug Bounty platforms: HackerOne, Bugcrowd, Intigriti

### 13.5 Databases & Intelligence
- Shodan - https://www.shodan.io/
- Censys - https://censys.io/
- GreyNoise - https://www.greynoise.io/
- VirusTotal - https://www.virustotal.com/
- AlienVault OTX - https://otx.alienvault.com/
- CVE Database - https://nvd.nist.gov/

### 13.6 Useful Sites & Services
- Certificate Transparency: crt.sh
- DNS history: SecurityTrails, ViewDNS
- Subdomain search: subdomains.io, crt.sh
- Tech fingerprint: Wappalyzer, BuiltWith
- Exploit DB: https://www.exploit-db.com/
- Packet Storm: https://packetstormsecurity.com/
- NVD - National Vulnerability Database

### 13.7 Learning Platforms
- Hack The Box - https://www.hackthebox.com/
- TryHackMe - https://tryhackme.com/
- PortSwigger Web Security Academy
- OffSec PEN-200
- eLearnSecurity

Appendix A: Wordlists, payloads, checklists
- Subdomain wordlists: SecLists
- Common directories: /admin, /backup, /config
- SQLi payloads: classic boolean, time-based
- XSS payloads: <svg onload=alert(1)>

Appendix B: Reporting templates
```
Finding ID: F-001
Title: ...
Severity: High
CVSS: 8.2
...
```

Appendix C: Legal references by jurisdiction
- US: CFAA 18 U.S.C. §1030
- EU: NIS2 Directive
- UK: Computer Misuse Act 1990

Appendix D: Daily Checklist
- [ ] Review scope
- [ ] Update recon notes
- [ ] Log all commands
- [ ] Take screenshots
- [ ] Verify impact

Appendix E: Red Team Rules
- No damage to production
- No data exfiltration beyond dummy
- Immediate stop on encountering safety triggers

*Last updated: 2026-11-01*
