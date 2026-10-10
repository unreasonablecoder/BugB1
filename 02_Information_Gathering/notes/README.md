# Module 01: Information Gathering & Reconnaissance
**Date:** 2026-10-10
**Target Scope:** `example-target.local` or IP Address

---

## 🧠 1. Concept & Vulnerability Theory
*Briefly explain what you are testing for in this section.*
* **Objective:** Find hidden directories, open ports, and exposed subdomains.
* **Impact:** Disclosing sensitive files or unmapped attack surfaces.

---

## 🛠️ 2. Reconnaissance & Enumeration Workflow
*Document the step-by-step logic you used to analyze the target.*

1. **Active Host Scanning:** Check for open web ports.
2. **Directory Brute-forcing:** Scan for hidden administration panels.

---

## 💻 3. Command Log & Exploit Payloads
*Keep your exact, reusable commands inside code blocks so you can copy-paste them later.*

### Network Scanning (Nmap)
```bash
# Aggressive service scan with default scripts on port 80/443
nmap -sV -sC -p 80,443 -oN nmap_web.txt <TARGET_IP>
```

### Directory Enumeration (Gobuster / Dirb)
```bash
# Fuzzing directories using a standard Parrot OS wordlist
gobuster dir -u http://<TARGET_IP>/ -w /usr/share/wordlists/dirb/common.txt -x php,txt,html
```

---

## 🛡️ 4. Burp Suite Evidence & Lab Walkthrough
*Document your practical lab victories here. Link local images from your screenshots folder.*

### Vulnerability Found: [Name of Vulnerability]
* **Observed Behavior:** The target application accepts modified parameters without server-side validation.
* **Proof of Concept (PoC) Request:**
  ```http
  GET /admin/config HTTP/1.1
  Host: target.local
  Cookie: session=attacker_session_cookie
  ```

### Visual Proof:
![Successful Exploit Confirmation](../screenshots/exploit_proof.png)

---

## 🔑 5. Remediation & Defensive Fix
*How do developers fix this issue?*
* Implement strict **Role-Based Access Control (RBAC)** on the server side.
* Ensure all sensitive administrative directories require explicit authentication tokens before rendering data.
