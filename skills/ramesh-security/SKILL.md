---
name: ramesh-security
description: "Security baseline for Indian apps: OWASP-aligned coding rules plus India-specific obligations (CERT-In 180-day logs, NTP sync, Aadhaar/PAN handling, RBI card and payment data rules, DPDP safeguards). Use when writing auth, APIs, storage, logging, payments, infra or reviewing security."
license: MIT
---

"Reasonable security safeguards" (DPDP s.8(5), IT Act s.43A/SPDI Rules 2011 until repealed) is judged after a breach. Be able to show you did the standard things.

## Code and design

- **AuthN:** argon2id/bcrypt/scrypt; MFA for admins and anything touching money or bulk personal data; OTP rate-limit, expiry (<=5 min), lockout, no OTP in logs or responses. SMS OTP alone is weak for high-risk actions.
- **AuthZ:** check object-level ownership on every request (IDOR/BOLA is the top real-world leak). Deny by default. Separate admin plane.
- **Input:** parameterised queries, output encoding, schema validation, size limits, safe file upload (type sniffing, random names, outside webroot, malware scan).
- **Sessions/tokens:** short-lived JWTs, rotate refresh tokens, httpOnly+Secure+SameSite cookies, CSRF protection.
- **Transport:** TLS 1.2+, HSTS, no mixed content, pin nothing you cannot rotate.
- **Secrets:** secret manager, no secrets in git/CI logs/mobile bundles; rotate on leak; run secret scanning in CI.
- **Crypto:** use libraries, AES-GCM/ChaCha20, KMS-managed keys, no home-grown schemes, no MD5/SHA1 for security.
- **Headers:** CSP, X-Content-Type-Options, frame-ancestors, Referrer-Policy.
- **Errors:** generic to user, detailed to logs (without personal data).
- **Supply chain:** pin and lock dependencies, SCA scan (Dependabot/osv-scanner), SBOM, review new packages, signed builds.
- **IaC/cloud:** no public buckets/DBs, least-privilege IAM, private subnets, WAF, backups tested, separate prod/non-prod. **Never copy production personal data to dev/staging** without masking.
- **LLM features:** treat prompts and outputs as data flows; do not send personal data to external models without a processor contract; guard against prompt injection and tool over-permission.

## India-specific

| Item | What to do |
|---|---|
| CERT-In Directions (28 Apr 2022) | Sync all system clocks to NIC/NPL NTP (or sources traceable to them). Keep ICT system logs **180 days, stored within India**, available to CERT-In on request. Report listed incidents in **6 hours** (see `ramesh-incident`). |
| DPDP safeguards | Access logs and breach-detection logs kept **>= 1 year**. Reconcile with CERT-In: keep the longer period; 180 days in India is the floor. |
| Aadhaar | Collect only if you are legally permitted (AUA/KUA or law-backed). Never store full number in plain; mask all but last 4; use Aadhaar Data Vault/reference tokens; do not display or log it; no Aadhaar-based denial of service where not mandated. Aadhaar Act s.29 bars sharing core biometrics. |
| PAN, bank, UPI IDs | Treat as financial identifiers: encrypt, mask in UI/logs, minimise. |
| Card data | Merchants/aggregators **must not store card numbers**; use network/issuer tokenisation (RBI card-on-file rules). PCI DSS for anything touching PAN. |
| Payment data localisation | RBI (2018): payment system data stored **only in India** (foreign processing allowed if deleted abroad and returned within the RBI-prescribed window). |
| Government/PSU clients | Often require MeitY-empanelled cloud and CERT-In empanelled auditor reports. |
| VPN / cloud / data-centre providers | CERT-In asks for subscriber/customer records for 5 years. |
| Critical sectors | NCIIPC guidelines for protected systems; SEBI CSCRF for regulated entities; RBI IT governance and cyber resilience directions for banks/NBFCs/PSOs; IRDAI information and cyber security guidelines. |

## Review heuristics (highest-value first)

1. Object-level authorisation on every ID-taking endpoint
2. Secrets or personal data in logs, URLs, analytics, crash reports
3. Public storage, unauthenticated internal admin/debug/Swagger/Actuator endpoints
4. SQL/NoSQL/command injection, SSRF, unsafe deserialisation
5. Missing rate limits on login, OTP, search, export
6. Backups unencrypted or unrestorable
7. Dependencies with known critical CVEs, abandoned packages
8. Mobile: hardcoded keys, cleartext traffic, exported components, no cert validation, data in backups

## Reply format

Fix it, don't lecture. For a finding: **what breaks, who is exposed, the one-line fix.**
