# Windows Event Log Analysis Notes

## What are Windows Event Logs?
Windows Event Logs record system activity such as logins, errors, security alerts, and system changes.

They help SOC analysts detect suspicious behavior.

---

## Key Log Types
| Log Type | Description |
|---|---|
| System Logs | OS and system services events |
| Application Logs | Software/app events |
| Security Logs | Login attempts, access events |

---

## Important Event IDs for Security Monitoring
| Event ID | Meaning |
|---|---|
| 4624 | Successful login |
| 4625 | Failed login |
| 4634/4647 | User logoff |
| 4688 | New process created |
| 4672 | Admin privilege assigned |

---

## Example Detection Case
### Suspicious Login Attempts
If many `4625` (failed login) events appear from the same IP/user in short time → possible brute-force attack.

---

## Next Steps
✅ Collect real sample logs  
✅ Analyze failed logins vs successful  
✅ Document findings  
