---
name: ramesh-audit
description: "Scan a repository for Indian compliance and security gaps (DPDP, CERT-In, secrets, PII in logs, consent, retention, licences) and produce a prioritised report with fixes. Use when asked to audit, assess readiness, or review a repo or PR for DPDP/security."
license: MIT
---

Produce a short, prioritised, evidence-based report. Every finding cites file and line.

## 1. Map the data (5 minutes)

- Find models/schemas/migrations, forms, API request bodies, analytics/crash SDK init, third-party clients (SMS, email, payments, LLM, maps), file uploads.
- List each personal-data field and where it flows: DB, cache, logs, queue, search, analytics, vendor, backup.
- Note hosting region from IaC/config.

## 2. Check (search, do not read the whole repo)

| Area | Look for |
|---|---|
| Secrets | API keys, tokens, `.env` committed, keys in mobile/web bundles, private keys |
| Logs | `console.log`/`logger` with request bodies, user objects, OTPs, tokens, Aadhaar/PAN/phone/email |
| Auth | missing ownership checks, weak hashing, no rate limit on login/OTP, long-lived tokens |
| Injection | string-built SQL, `eval`, shell exec with user input, unsafe deserialisation, SSRF |
| Storage | public buckets, unencrypted sensitive columns, Aadhaar stored raw, card data stored |
| Consent | pre-ticked boxes, no consent record, analytics firing before consent, no withdrawal |
| Children | no age gate in a consumer app, ads/tracking SDKs in a kids-facing app |
| Rights | no export, delete, or correction path; delete leaves rows in logs, search, analytics |
| Retention | no TTL/purge for sessions, OTPs, uploads, inactive accounts |
| Third parties | SDKs sending device IDs or PII abroad; no processor list |
| Breach readiness | no incident doc, no log retention config (180 days, India), no NTP |
| Dependencies | known CVEs (`npm audit`, `pip-audit`, `osv-scanner`), copyleft licences in closed code |
| Legal surface | privacy policy / ToS / grievance officer contact missing; dark patterns |

Use the project's own scanners if present. Do not install tools unless asked.

## 3. Report

```
# Ramesh audit: <repo>   (date, commit)
Scope and assumptions: ...
Data map: <table of field -> purpose -> stores -> vendors>

## Critical / High / Medium / Low
1. [High] <title>, <file>:<line>
   Impact: <who is exposed / which law>
   Fix: <one concrete action>

## Not checked
...
## Next 30 days (top 5 actions)
```

Severity: **Critical** = exploitable leak of personal/financial data or secrets in repo. **High** = missing core duty (consent, breach path, erasure) or serious vuln. **Medium** = weak control. **Low** = hygiene.

Be honest about what was not checked. Do not claim "compliant"; claim "no gaps found in X".
