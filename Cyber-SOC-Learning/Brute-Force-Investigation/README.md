# Windows Event Logs Investigation - Brute Force Attack

### 🔍 Objective
Analyze Windows Security Event Logs to detect brute-force login attempts.

### 📌 Target Event IDs
- 4625 — Failed login attempt
- 4624 — Successful login
- 4672 — Admin privilege assigned

### ✅ Steps Performed
1️⃣ Collected Windows security logs  
2️⃣ Filtered Event ID 4625  
3️⃣ Identified repeated login attempts from same user/IP  
4️⃣ Checked for Event ID 4624 after failures  
5️⃣ Documented findings in Incident Report  

### Files in this folder
- FailedLogins_4625.evtx — exported failed login events
- SuccessLogins_4624.evtx — exported successful login events (if present)
- Findings.md — summary & recommendations


### 📊 Findings Summary
- Repeated failed logins suggest possible brute-force attack  
- Need further monitoring and blocking if pattern continues  

### 📝 Next File
Incident Report will be attached in this folder
