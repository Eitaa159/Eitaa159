# Findings — Windows Brute-Force Investigation

## Executive summary
On **Nov 6, 2025**, a short series of failed Windows authentication attempts was observed and analyzed.  
A total of **4 failed logon events (Event ID 4625)** were recorded within a **15-second window** (13:38:27 → 13:38:42). All events originated from **127.0.0.1 (localhost)** and targeted the machine account **DESKTOP-04AB8AQ$**. No successful authentication followed the failures.

**Conclusion:** Low-severity / local brute-force simulation. No evidence of compromise.

---

## Technical details

- **Event types reviewed:**  
  - 4625 — Failed logon  
  - 4624 — Successful logon (checked; none correlated to these failures)

- **Total failed attempts (4625):** 4  
- **Time window:** 2025-11-06 13:38:27 → 2025-11-06 13:38:42 (approx. 15 seconds)  
- **Source IP(s):** 127.0.0.1 (localhost)  
- **Targeted account(s):** DESKTOP-04AB8AQ$ (machine account)  
- **Files added to repository:**  
  - `FailedLogins_4625.evtx` — exported failed login events  
  - `FailedLogins_4625_parsed.csv` — parsed CSV extract of key fields  
  - `SuccessfulLogins_4624.evtx` / `SuccessfulLogins_4624_parsed.csv` (if present)

---

## Analysis & interpretation
- The attempts are local (127.0.0.1) and target a machine account rather than an interactive user account. This pattern is consistent with a **local test or automated script** running on the host rather than an external unauthorized actor.
- The short duration and low count (4 attempts) indicate either a quick manual test or a very limited automation attempt. No subsequent successful logon suggests the attempt failed to obtain valid credentials.
- Given the local source and targeted account type, the risk of lateral movement or data exfiltration from these events alone is **low**.

---

## Severity
**Low** — local, unsuccessful attempts with no follow-on suspicious activity. Escalate to **Medium/High** only if:
- Attempts reappear at higher volume, or
- Attempts originate from external IPs, or
- Privileged accounts are targeted and succeeded.

---

## Recommendations
1. **Immediate**
   - Confirm this activity with the system owner (was this a scheduled test/scan?).  
   - Preserve the EVTX and parsed CSV files for audits: `FailedLogins_4625.evtx`, `FailedLogins_4625_parsed.csv`.

2. **Preventive**
   - Enforce an account lockout policy (e.g., lock after N failed attempts within M minutes).  
   - Enable/verify MFA for privileged and remote accounts.

3. **Detection**
   - Add a SIEM rule: alert on `> 3 failed logons within 1 minute` from the same source IP or username.  
   - Create a dashboard metric tracking failed logons by source and by account.

4. **Investigation**
   - If future events show external IPs, collect network captures and correlate with firewall/VPN logs.  
   - Parse EVTX into a CSV (already provided) and extract top offender IPs / usernames and a timeline for reporting.

---

## Next steps (suggested)
- Confirm whether the activity was a planned test. If so, annotate the incident in the repo and close.  
- If not confirmed, continue monitoring for recurrence and apply account lockout rules.  
- Optionally, perform a broader sweep for Event ID 4625 occurrences over the last 30 days and report trends.

---

## Notes on artifacts & privacy
EVTX files may include usernames and IP addresses. If publishing these artifacts elsewhere, consider sanitizing sensitive fields (e.g., mask IPs or anonymize usernames).
