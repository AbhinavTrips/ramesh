---
name: ramesh-legal
description: "Legal essentials for Indian app and SaaS builders: IT Act, IT Rules 2021 intermediary duties, consumer protection and dark patterns, e-commerce rules, Aadhaar, IP and open-source licences, sector regulators (RBI, SEBI, IRDAI, health, telecom), ToS and privacy policy. Use when shipping user-facing flows, terms, payments, marketplaces, content, or choosing licences."
license: MIT
---

Not legal advice. This tells a developer which law is probably in play so they can ask the right question early.

## Core statutes

| Law | Why a dev cares |
|---|---|
| **Information Technology Act 2000** | s.43 / s.66 (unauthorised access, damage), s.66C/66D (identity theft, cheating by impersonation), s.67 (obscene content), s.69 (govt interception and decryption orders), s.69A (blocking), s.72A (disclosure in breach of contract), s.79 (intermediary safe harbour). s.43A and SPDI Rules 2011 govern sensitive personal data until DPDP repeals them. |
| **DPDP Act 2023 + Rules 2025** | See `ramesh-dpdp`. |
| **IT (Intermediary Guidelines and Digital Media Ethics Code) Rules 2021** | If users post/share content: publish rules and privacy policy, appoint a grievance officer in India, acknowledge complaints in 24h and resolve within 15 days, remove flagged non-consensual intimate imagery within 24h, follow takedown orders. Large social platforms: extra duties (traceability, compliance officers, monthly reports). |
| **Bharatiya Nyaya Sanhita 2023** | Replaced IPC; cheating, forgery, defamation and organised-crime provisions apply to online conduct. |
| **Consumer Protection Act 2019 + E-Commerce Rules 2020** | Display seller details, price breakup, return/refund policy, grievance officer, country of origin; no unfair trade practices, fake reviews, or drip pricing; no manipulating search ranking without disclosure. |
| **CCPA Guidelines on Dark Patterns 2023** | Banned: false urgency, basket sneaking, confirm-shaming, forced action, subscription traps, interface interference, bait-and-switch, drip pricing, disguised ads, nagging, trick questions, SaaS billing traps, rogue malware. Consent flows must not use these either. |
| **Copyright Act 1957, Trade Marks Act 1999, Patents Act 1970** | Ownership of code by employees and contractors needs a written assignment; section 17 default employer ownership does not cover freelancers. Check trademark before naming a product. Software as such is not patentable. |
| **Indian Contract Act 1872 / Stamp Acts** | E-signed ToS is enforceable; clickwrap beats browsewrap; stamp duty on agreements is state-specific. Unfair or one-sided terms may not hold in consumer cases. |
| **Rights of Persons with Disabilities Act 2016** | Government and many private services must be accessible; follow GIGW/WCAG 2.1 AA. |
| **Telecom Act 2023** | OTT/communications, SIM/identity verification, lawful intercept duties; SMS/DLT registration for commercial messages under TRAI rules (templates, headers, consent, DND). |
| **Companies Act 2013, Labour codes** | Data-leak from an employee, POSH Act 2013 for the workplace, employment contracts with IP and confidentiality clauses. |
| **Information security of government work** | MeitY, CERT-In empanelment, GIGW, state data centre or MeitY-empanelled cloud when serving government. |

## Sector regulators

- **Fintech / payments (RBI):** Payment aggregator and gateway authorisation; payment data localisation; no card storage by merchants; KYC/CKYC; digital lending directions (disclosures, KFS, no auto-debit without consent, lending service providers and DLA reporting, direct disbursal to the borrower's bank account); outsourcing and IT governance rules; UPI via NPCI rules; fraud and customer-liability rules.
- **Securities (SEBI):** Cybersecurity and Cyber Resilience Framework (CSCRF), algorithmic trading rules, research analysts/investment adviser rules, finfluencer restrictions.
- **Insurance (IRDAI):** Cybersecurity guidelines, outsourcing, data localisation for policyholder data (as per IRDAI regulations).
- **Health:** Telemedicine Practice Guidelines 2020 (registered practitioners), ABDM Health Data Management Policy and consent artefacts, DISHA not enacted, Clinical Establishments rules; e-pharmacy under Drugs and Cosmetics Rules.
- **Education/minors:** Parental consent and no tracking of children under DPDP; UGC/AICTE rules for ed-tech degrees.
- **Gaming/gambling:** Online Gaming rules; real-money games are heavily restricted under recent law; get counsel before launching.
- **Crypto/VDA:** Registration with FIU-IND as reporting entity, KYC/AML (PMLA), TDS and tax reporting.
- **Telecom/messaging:** TRAI TCCCPR for commercial SMS/calls.

## Dev practices with legal weight

- **Privacy policy and ToS:** match the real data flows. A policy that promises what the code does not do is a misrepresentation. Version them; show the change to users.
- **Open-source licences:** keep an SBOM; record each dependency licence; GPL/AGPL/SSPL in closed SaaS needs a review; attribute MIT/Apache; no copy of Stack Overflow/GitHub code without licence check (CC BY-SA applies to SO snippets).
- **Contractors/employees:** signed IP assignment + NDA before they commit code.
- **AI-generated code and data:** you stay responsible for output; train/finetune only on data you have rights to and purpose for; do not paste customer personal data into public AI tools.
- **Scraping:** check ToS and personal-data implications; publicly available personal data is not free-for-all under DPDP for non-personal-domestic use.
- **Email/SMS marketing:** consent, unsubscribe in every message, DLT templates for SMS.
- **Records:** keep invoices, GST data, KYC per sectoral retention periods before purging for DPDP erasure; retention required by law overrides deletion.
- **Dispute/jurisdiction:** choose Indian law and a seat; mention arbitration only if you will really use it.

## Reply format

For a legal-sensitive change, add **Compliance notes** listing the law, the specific dev action, and "confirm with counsel" only where the call is a judgement.
