# Ramesh: Indian compliance rules for developers

Always-on guardrails for AI coding agents and humans. Applies to any app: DPDP Act, IT Act, CERT-In, sector rules. Full detail is in [skills/](./skills). Not legal advice.

## Before you write
1. Touches personal data (name, phone, email, Aadhaar, PAN, location, device ID, health, finance)? Follow `skills/ramesh-dpdp/SKILL.md`.
2. Auth, secrets, uploads, payments, public endpoints? Follow `skills/ramesh-security/SKILL.md`.
3. Sends data to a third party (analytics, LLM, SMS, crash SDK)? Name vendor, data, country; it is a processor and needs a contract.
4. Regulated sector (fintech, health, insurance, securities, minors)? See `skills/ramesh-legal/SKILL.md`.

## Rules
- Collect less: every field needs a purpose.
- Consent: specific, itemised, unbundled, no pre-ticked boxes, withdrawable as easily as given; store a consent record (user, purpose, notice version, time).
- Under 18: verifiable parental consent; no tracking or targeted ads.
- Never log personal data, tokens, OTPs, passwords, card or Aadhaar numbers.
- Never store CVV, card numbers (use tokenisation), raw Aadhaar, or plaintext passwords.
- Secrets only in a secret manager or env; never in repo, client bundle, or mobile app.
- TLS 1.2+, encryption at rest for personal data, argon2id/bcrypt for passwords.
- Check object-level authorisation on every endpoint taking an ID.
- Every personal-data table needs a retention period and a delete path; build access, correction, erasure, and nominee endpoints.
- Keep logs 180 days in India (CERT-In), at least 1 year for DPDP breach investigation; sync clocks to NIC/NPL NTP.
- Breach: report to CERT-In within 6 hours; notify DPDP Board and users without delay, detailed Board report within 72 hours (`skills/ramesh-incident/SKILL.md`).
- Payment data stays in India (RBI); never copy production personal data to dev/staging.
- Check dependency licences (GPL/AGPL in closed code is a risk).
- No dark patterns in consent or checkout.

## Reply
Do the task, then add 1-3 lines "Compliance notes": assumptions, what was not checked, what a lawyer/DPO must confirm. Never invent section numbers or deadlines; say "verify".
