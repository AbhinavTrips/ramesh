# Ramesh

Open-source **Skills for AI coding agents and developers building in India**: DPDP Act, IT Act, CERT-In, and security basics, so teams are not caught off guard.

> Not legal advice. Engineering guidance by the community. Verify with counsel and official sources.
> **Last reviewed:** 2026-11 (DPDP Rules 2025 phased timelines; always re-check meity.gov.in).

## Why

The DPDP Act carries penalties up to ₹250 crore, CERT-In wants incident reports in 6 hours, and most small teams have never read either. Ramesh puts the rules where the code is written.

## Skills

| Skill | Covers |
|---|---|
| [ramesh](./skills/ramesh/SKILL.md) | Always-on guardrails, lightweight |
| [ramesh-dpdp](./skills/ramesh-dpdp/SKILL.md) | Notice, consent, children, erasure, breach, SDF, penalties as a dev checklist |
| [ramesh-security](./skills/ramesh-security/SKILL.md) | OWASP-style coding rules + CERT-In logs/NTP, Aadhaar, RBI card & payment data |
| [ramesh-incident](./skills/ramesh-incident/SKILL.md) | 6-hour CERT-In, DPDP Board/user notice, sector regulators runbook |
| [ramesh-legal](./skills/ramesh-legal/SKILL.md) | IT Act, intermediary rules, consumer law and dark patterns, IP/open source, sector regulators |
| [ramesh-audit](./skills/ramesh-audit/SKILL.md) | Scan a repo and get a prioritised report |

## Install

Works with any agent that reads `SKILL.md` or `AGENTS.md`.

```bash
# Copy skills into your project (Claude Code / Copilot / Codex style)
git clone https://github.com/AbhinavTrips/ramesh && cp -r ramesh/skills <your-repo>/.claude/skills   # or .github/skills, .agents/skills
# Always-on rules
cp ramesh/AGENTS.md <your-repo>/AGENTS.md            # Cursor: .cursor/rules/ramesh.mdc, Copilot: .github/copilot-instructions.md
```

Then ask: *"Run ramesh-audit on this repo"* or *"Add signup with DPDP-compliant consent"*.

## Roadmap

- Sector skills: fintech (RBI), health (ABDM), edtech/minors, gaming
- Consent-UI and consent-ledger code patterns per stack
- CI check for PII in logs and secrets
- Hindi and regional-language notice templates
- Legal review by practising lawyers (most wanted)

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Every legal claim needs an official source.

Inspired by [ponytail](https://github.com/DietrichGebert/ponytail). MIT licensed.
