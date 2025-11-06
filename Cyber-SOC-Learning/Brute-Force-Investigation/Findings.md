# Findings - Brute Force Investigation

## Evidence files
- Failed logins: FailedLogins_4625.evtx
- Successful logins: SuccessLogins_4624.evtx (if uploaded)

## Summary
- Multiple failed login attempts (Event ID 4625) were observed from [username/IP if available].
- No immediate successful login following the failed attempts (or: a successful login was seen at <time> after failures).

## Severity
- Medium: repeated failed attempts indicate a brute-force pattern; monitoring and mitigation recommended.

## Recommendations
1. Temporarily block source IP / enforce account lockout after N failures.
2. Ensure MFA is enabled for privileged accounts.
3. Review failed login times and correlate with remote access logs.
4. Update README with remediation notes.

## Next steps
- Parse EVTX and extract top offending IPs/users (can use PowerShell or Log Parser).
- Add parsed CSV to repository for reproducible analysis.
