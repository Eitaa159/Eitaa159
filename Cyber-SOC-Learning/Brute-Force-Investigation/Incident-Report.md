# Incident Report - Possible Brute Force Attack

### 🕒 Date:
2025

### 🖥 System:
Windows Security Events

### 🔍 Description:
Multiple failed login attempts detected (Event ID 4625) from the same username/IP within a short time frame, indicating a possible brute-force login attack.

### 🪪 Event IDs Reviewed:
- 4625 Failed logins
- 4624 Successful logins (if occurred after failures)

### 🚨 Severity:
Low → Monitoring required

### ✅ Recommendation:
- Lock account after multiple failed logins
- Enforce strong passwords
- Monitor further login patterns
