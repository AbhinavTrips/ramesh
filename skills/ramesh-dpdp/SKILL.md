---
name: ramesh-dpdp
description: "Engineering checklist for the Digital Personal Data Protection Act 2023 and DPDP Rules 2025: notice, consent, children, erasure, breach, grievance, Significant Data Fiduciary. Use when building signup, forms, profiles, analytics, marketing, KYC, or deletion flows."
license: MIT
---

Turn the DPDP Act into code and tickets. You are a **Data Fiduciary** if you decide why and how personal data is processed (almost every app company). Vendors who process on your behalf are **Data Processors**.

Applies to digital personal data processed in India, and outside India if offering goods/services to people in India.
Timeline: the Rules were notified in Nov 2025 and obligations phase in (Board set-up first, consent managers next, most fiduciary duties about 18 months after notification). **Verify current dates on meity.gov.in; start now because retrofits are expensive.**

## 1. Notice (Act s.5)

- Shown before or at the time of consent request, in plain language, with an option to read in English or any of the 22 Eighth Schedule languages.
- Must state: the personal data collected, the purpose, how to exercise rights, how to complain to the Board.
- Build: versioned notice text, stored with each consent record. Legacy users need a fresh notice too.

## 2. Consent (s.6) and legitimate uses (s.7)

- Free, specific, informed, unconditional, unambiguous, clear affirmative action. Only data necessary for the stated purpose.
- No bundling "accept all or can't use app". Separate toggles for optional purposes (marketing, analytics).
- Withdrawal as easy as giving; after withdrawal stop processing (and make processors stop) within a reasonable time.
- Some uses need no consent (s.7): voluntarily given for a purpose, state benefits, legal obligation, medical emergency, employment, etc. Do not stretch "legitimate use" to cover marketing or analytics.
- Consent record schema: `user_id, purpose, notice_version, language, granted_at, withdrawn_at, channel/ip/ua`.
- A registered **Consent Manager** may be used; design your consent API so it can integrate.

## 3. Children and persons with disability (s.9)

- Under 18: verifiable parental/guardian consent before processing. No tracking, behavioural monitoring, or targeted ads aimed at children. (Classes of fiduciaries such as healthcare and education have limited exemptions in Rules; confirm.)
- Build: age gate at signup, guardian verification flow, separate data path with ads/analytics disabled.

## 4. Security safeguards (s.8(5))

Reasonable safeguards are mandatory and the highest penalty (up to ₹250 crore) attaches here. At minimum: encryption/obfuscation/tokenisation, access control, logging and monitoring of access, backups and continuity, and **retaining logs and relevant data for one year** for detecting and investigating breaches (per Rules). Contracts with processors must require the same. See `ramesh-security`.

## 5. Breach (s.8(6))

Notify the Data Protection Board **and each affected user**, without delay, with a detailed report to the Board within 72 hours (per Rules). Runbook in `ramesh-incident`. Failure: up to ₹200 crore.

## 6. Accuracy, retention, erasure (s.8(3), 8(7), s.12)

- Keep data accurate if used for decisions or shared.
- Erase when consent is withdrawn or the purpose is no longer served, unless law requires retention. Tell the processors to erase too.
- Rules require giving users advance notice before erasing for inactivity (about 48 hours; verify) in specified categories like e-commerce, gaming, social media above thresholds.
- Build: `retention_policy` per table, a scheduled purge job, a user-initiated "delete my account" that cascades to processors, search indexes, caches, and analytics. Document what backups do.

## 7. Data principal rights (ss.11-14)

Provide in-product, easy ways for: access (summary of data and who it was shared with), correction/completion/updating, erasure, grievance redressal, and **nominating** another person for death/incapacity. Respond within the time the Rules set (grievances: within 90 days max; aim for far less).

## 8. Accountability

- Publish contact of a **DPO** (Significant Data Fiduciaries) or a person who can answer questions (all fiduciaries) in notice and app.
- Have a **grievance redressal** channel and respond before the user goes to the Board.
- Keep a **data inventory / RoPA** even if not strictly required; you cannot do the above without it.

## 9. Significant Data Fiduciary (s.10)

Government notifies based on volume, sensitivity, risk. Extra: India-based DPO, independent data auditor, annual DPIA and audit, algorithmic due diligence, and possible data localisation for specified categories. If you have millions of users or sensitive data, design for this from day one.

## 10. Cross-border (s.16) and exemptions (s.17)

Transfers are allowed except to countries the government restricts (negative list). Sector laws can be stricter (RBI, SEBI, IRDAI, health). Record where each processor stores data.

## 11. Penalties (Schedule)

Up to ₹250 cr (safeguards), ₹200 cr (breach notice, children), ₹150 cr (SDF duties), ₹50 cr (other), ₹10,000 for users' duty breach. Penalties are per instance and the Board looks at gravity, repetition, mitigation.

## Developer quick checklist

- [ ] Data inventory: field, purpose, lawful basis, retention, processors, location
- [ ] Notice + consent UI, itemised, versioned, multilingual-ready
- [ ] Consent ledger + withdrawal endpoint wired into marketing/analytics/processors
- [ ] Age gate + parental consent path
- [ ] Access / correction / erasure / nominate endpoints
- [ ] Retention jobs and inactivity erasure notice
- [ ] Log masking, encryption, RBAC, access audit log with 1-year retention
- [ ] Processor contracts and sub-processor list
- [ ] Breach runbook and contact owners
- [ ] Grievance officer / DPO contact in app and website
- [ ] No dark patterns around consent (see `ramesh-legal`)
