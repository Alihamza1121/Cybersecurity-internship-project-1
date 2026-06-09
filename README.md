# 🔐 Cyber Security Internship 2026

**Author:** Wahab Shahbaz  
**Program:** Cybersecurity Internship 2026  
**Repository:** [GitHub - Cyber-Security-Internship-2026](https://github.com/wahabshahbaz/Cyber-Security-Internship-2026)

&gt; ⚠️ **Disclaimer:** This project is for **educational purposes only**. All security testing was performed on locally hosted and self-owned environments. Do not use these techniques on systems without explicit authorization.

---

## 📋 Project Overview

This repository contains the complete work for a 6-week Cybersecurity Internship program. The project demonstrates practical implementation of security auditing, vulnerability assessment, penetration testing, and secure deployment practices on a full-stack web application.

**Application Stack:** Node.js / Express / MongoDB / React  
**Local URL:** `http://localhost:3000`  
**Production URL:** `https://cyber-security-internship-2026-production.up.railway.app`

---

## ✅ Week-wise Progress

### Week 1-4: Foundation & Vulnerability Assessment
- Environment setup and secure coding practices
- Input validation and sanitization implementation
- Authentication and session management

### Week 5: Web Application Security Testing
| Tool | Purpose | Status | Evidence |
|------|---------|--------|----------|
| Nikto | Web server vulnerability scan | ✅ Complete | `week5-nikto-retest.html` |
| Burp Suite Repeater | CSRF token bypass testing | ✅ Complete | Week 5 screenshots |

### Week 6: Advanced Security Audits & Final Deployment

#### 1. Security Audits & Compliance
| Tool | Purpose | Status | Evidence |
|------|---------|--------|----------|
| **OWASP ZAP** | Full application automated scan | ✅ Complete | `WEEK6_ZAP_Report.html` |
| **Nikto** | Web server configuration audit | ✅ Complete | `week5-nikto-retest.html` |
| **Lynis** | System-level security hardening audit | ✅ Complete | `WEEK6_Lynis_Retest.txt` |

**Lynis Hardening Score:** `70/100` (Baseline: 63 → Remediated: 70)  
**Key Fixes Applied:**
- SSH hardening (Port 2222, MaxAuthTries=3, disabled X11/Agent forwarding)
- GRUB bootloader password protection
- AppArmor MAC framework enabled
- PHP `allow_url_fopen` disabled
- Kernel sysctl hardening applied
- Malware scanner (rkhunter) installed

#### 2. Secure Deployment Practices
| Task | Status | Evidence |
|------|--------|----------|
| **Docker containerization** | ✅ Complete | `Dockerfile`, `.dockerignore` |
| **Trivy vulnerability scan** | ✅ Complete | `WEEK6_Trivy_Scan.txt` |
| **Auto security updates** | ✅ Complete | `unattended-upgrades.conf` |

#### 3. Final Penetration Testing
| Test | Tool | Status | Evidence |
|------|------|--------|----------|
| **Login brute force** | Burp Suite Intruder | ⬜ Pending | Screenshots |
| **CSRF token bypass** | Burp Suite Repeater | ✅ Complete | Week 5 screenshots |
| **Business logic test** | Manual / DevTools | ✅ Complete | `business_logic_evidence/` |

**Business Logic Findings:**
- IDOR testing on user profiles via parameter manipulation
- Admin endpoint access control verification
- Client-side parameter tampering assessment
- Workflow bypass attempts on authentication flow

#### 4. Deployment Status
| Environment | URL | Status |
|-------------|-----|--------|
| Local Development | `http://localhost:3000` | ✅ Running |
| **Production** | `https://cyber-security-internship-2026-production.up.railway.app` | ✅ **Live** |

---

## 📁 Repository Structure


---

## 🛡️ Security Measures Implemented

### Application Layer
- Input validation and parameterized queries
- Secure session management
- CSRF protection tokens
- Security headers implementation

### System Layer
- Lynis-guided hardening (Score: 70/100)
- SSH non-default port & key-based restrictions
- Firewall (iptables/ufw) active
- Fail2ban intrusion prevention enabled
- AppArmor mandatory access control enabled
- Automatic security updates configured

### Deployment Layer
- Docker containerization with minimal attack surface
- Trivy container image vulnerability scanning
- Production deployment on Railway.app with HTTPS
- Environment variable isolation

---

## 📊 Security Audit Summary

| Category | Status |
|----------|--------|
| Web Application Scan (ZAP) | ✅ Completed |
| Server Configuration (Nikto) | ✅ Completed |
| System Hardening (Lynis) | ✅ Completed (70/100) |
| Container Security (Trivy) | ✅ Completed |
| Manual Penetration Testing | ✅ Partially Completed |
| Production Deployment | ✅ Live |

---

## 🚀 How to Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/wahabshahbaz/Cyber-Security-Internship-2026.git
cd Cyber-Security-Internship-2026

# 2. Install dependencies
npm install

# 3. Start the application
npm start

# 4. Access the app
# Open browser → http://localhost:3000

---

# Build the image
docker build -t cyber-security-app .

# Run the container
docker run -p 3000:3000 cyber-security-app

# Scan with Trivy
trivy image cyber-security-app

---


