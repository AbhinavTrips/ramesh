---
name: ramesh-incident
description: "Incident and data-breach response runbook for India: CERT-In 6-hour reporting, DPDP Board and user notification, sector regulator reporting, evidence preservation. Use when there is a suspected breach, leak, ransomware, account takeover, or when writing an incident plan."
license: MIT
---

A breach in India can trigger several clocks at once. Start all of them; do not wait for certainty.

## Clocks

| Who | When | Trigger |
|---|---|---|
| **CERT-In** (incident@cert-in.org.in, phone/fax on cert-in.org.in) | **Within 6 hours** of noticing | Any listed incident type: targeted scanning, compromise of critical systems, unauthorised access to IT systems or data, defacement, malicious code/ransomware, data breach or leak, attacks on servers/apps/IoT/cloud/AI-ML, identity theft/spoofing/phishing, fake mobile apps, attacks on digital payment systems, etc. |
| **DPDP Board** | Without delay, then detailed report within **72 hours** | Personal data breach (Rules; verify current in-force date) |
| **Affected users** | Without delay, plain language | Personal data breach |
| **Sector regulator** | Per circular, often hours | RBI (banks/NBFC/PSOs: typically within 2-6 hours of detection for cyber incidents), SEBI (6 hours for regulated entities), IRDAI (6 hours), telecom/DoT, NCIIPC for protected systems |
| **Police / cyber cell** | Promptly for crimes (extortion, fraud) | cybercrime.gov.in, 1930 for financial fraud |
| **Customers/enterprise clients** | Per contract | Many MSAs require 24-72 hours |

## First hour

1. **Declare** an incident, name an incident commander and a scribe, open a timeline doc (UTC + IST).
2. **Preserve evidence** before cleaning: snapshot disks/VMs, export logs, freeze log retention, do not reboot or wipe unless needed to stop damage.
3. **Contain:** revoke tokens/keys/sessions, disable compromised accounts, isolate hosts, block egress, rotate secrets.
4. **Report to CERT-In** with what you know (even partial). Update later; late is worse than incomplete.
5. **Scope:** what data, how many people, which categories (personal, financial, health, children), since when, is it still happening.

## Notification content (users)

What happened, which of their data, likely consequences, what you did, what they should do (reset password, watch for phishing, block card), a contact person. No victim blaming, no legalese.

## Notification content (Board / CERT-In)

Nature, extent, timing, location and likely impact of the breach; people affected; mitigation taken; findings on who caused it if known; remedial steps; safeguards to prevent recurrence; sequence of events.

## After

- Root-cause analysis, blameless, within 2 weeks; track fixes to done.
- Update the data inventory, processor contracts, and detection rules.
- Keep records: they are your "reasonable safeguards" evidence.
- Test the plan: run a tabletop twice a year including the 6-hour report drill.

## Make it ready before it happens

- [ ] Named owner for CERT-In and DPDP reporting plus a backup
- [ ] Contact list: legal counsel, forensic firm, cloud support, cyber insurer, PR
- [ ] Logs retained 180 days in India, clocks NTP-synced
- [ ] Notification templates pre-approved (Board, user, enterprise client)
- [ ] Pre-built "kill switch" for tokens/keys and an account-wide forced logout
- [ ] Tested backups, offline copy
