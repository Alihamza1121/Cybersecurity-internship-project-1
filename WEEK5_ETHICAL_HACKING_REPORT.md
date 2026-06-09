# Week 5: Ethical Hacking & Exploiting Vulnerabilities

## 🎯 Goal
Learn ethical hacking techniques, exploit vulnerabilities in a test environment, and enhance application security.

---

## 1. Ethical Hacking Basics — Reconnaissance

### Passive Reconnaissance
| Tool | Command | Finding |
|------|---------|---------|
| `whois` | `whois localhost` | No public whois for localhost (expected) |
| `dig` | `dig localhost` | Resolves to 127.0.0.1 |
| `whatweb` | `whatweb http://localhost:3000` | Node.js/Express detected, security headers active |

**Technology Fingerprinting Results:**
- **Framework:** HTML5, Express.js
- **Security Headers:** HSTS, CSP, X-Frame-Options, X-XSS-Protection
- **Information Disclosure:** Page title "Secure App - Home"

### Active Reconnaissance
| Tool | Command | Finding |
|------|---------|---------|
| `nmap` | `nmap -sS -O -sV localhost` | Port 22 (SSH), Port 3000 (Node.js) |
| `nikto` | `nikto -h http://localhost:3000` | CSRF cookie missing HttpOnly (FIXED) |

**Nmap Key Findings:**
- **Open Ports:** 22/tcp (OpenSSH), 3000/tcp (Node.js/Express)
- **OS:** Linux 5.10 - 6.2 (Kali Rolling)
- **Security Headers Verified via Nmap:** CSP, HSTS, X-Frame-Options active

---

## 2. SQL Injection & Exploitation (SQLMap)

### Vulnerable Endpoint Testing
| Test | Command | Result |
|------|---------|--------|
| Basic scan | `sqlmap -u "http://localhost:3000/test-sqli?id=1" --batch --level=1` | ✅ VULNERABLE — UNION query |
| Deep scan | `sqlmap -u "http://localhost:3000/test-sqli?id=1" --batch --level=3 --risk=2` | ✅ DBMS: SQLite |
| DB enumeration | `sqlmap -u "http://localhost:3000/test-sqli?id=1" --dbs --batch` | ⚠️ SQLite limitation |
| Table dump | `sqlmap -u "http://localhost:3000/test-sqli?id=1" -D database_name --tables --batch` | ✅ Tables: `sqlite_sequence`, `users` |

**Critical Finding:** `users` table discovered containing credential data.

### Root Cause (Vulnerable Code)
```javascript
// INTENTIONALLY VULNERABLE — FOR TESTING ONLY
db.get(`SELECT * FROM users WHERE id = ${id}`, (err, row) =&gt; { ... });

// SECURE — Week 2 Implementation
db.get(`SELECT * FROM users WHERE username = ?`, [username], (err, user) => { ... });

| Test         | Command                                                                        | Result           |
| ------------ | ------------------------------------------------------------------------------ | ---------------- |
| Retest login | `sqlmap -u "http://localhost:3000/login?username=admin&password=test" --batch` | ✅ NOT INJECTABLE |


+ /: Cookie 'csrf' created without httponly flag

// BEFORE
const csrfProtection = csrf({ cookie: true });

// AFTER
const csrfProtection = csrf({ 
    cookie: {
        httpOnly: true,
        sameSite: 'strict',
        secure: false
    } 
});


+ /: Cookie 'csrf' created with httponly flag   ✅

| # | Vulnerability                  | Severity    | Tool    | Status              |
| - | ------------------------------ | ----------- | ------- | ------------------- |
| 1 | SQL Injection (test endpoint)  | 🔴 Critical | SQLMap  | ✅ Exploited & Fixed |
| 2 | CSRF Cookie Missing HttpOnly   | 🟠 High     | Nikto   | ✅ Fixed             |
| 3 | Information Disclosure (title) | 🟡 Low      | whatweb | ℹ️ Accepted Risk    |


| File                      | Description                   |
| ------------------------- | ----------------------------- |
| `week5-nmap-scan.txt`     | Nmap port/service scan        |
| `week5-nikto-scan.html`   | Initial Nikto web scan        |
| `week5-nikto-retest.html` | Post-fix Nikto scan           |
| `week5-sqlmap-report.txt` | SQLMap injection test results |



**Save:** `Ctrl+O` → `Enter` → `Ctrl+X`

---

## 🔴 Step 2: README.md Mein Week 5 Section Add Karo

```bash
nano README.md


---

## 🎯 Week 5: Ethical Hacking & Exploiting Vulnerabilities

### 🔍 1. Reconnaissance

**Passive:**
- `whois`, `dig`, `whatweb` — Technology fingerprinting
- Security headers detected: HSTS, CSP, X-Frame-Options

**Active:**
- `nmap` — Ports 22 (SSH), 3000 (Node.js) discovered
- `nikto` — Web vulnerability scan

### 💉 2. SQL Injection (SQLMap)

| Phase | Result |
|-------|--------|
| **Exploitation** | `/test-sqli?id=1` — UNION query injection confirmed |
| **Data Extraction** | Tables: `sqlite_sequence`, `users` |
| **Fix** | Parameterized queries (`?` placeholders) |
| **Verification** | SQLMap: "not injectable" on secured endpoints |

### 🛡️ 3. CSRF Protection

| Phase | Finding | Status |
|-------|---------|--------|
| **Initial Scan** | Cookie missing `HttpOnly` flag | ⚠️ Found |
| **Fix** | `csrf({ cookie: { httpOnly: true } })` | ✅ Applied |
| **Retest** | Nikto warning resolved | ✅ Verified |

### 📄 Full Report
👉 [WEEK5_ETHICAL_HACKING_REPORT.md](WEEK5_ETHICAL_HACKING_REPORT.md)

