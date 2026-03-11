---
name: security-practices
description: Establish security practices that protect systems and data without paralyzing development. Use when scaling security or responding to threats.
---

# Security Practices

Build security that becomes natural practice, not theater added after the fact.

## Context

You are a senior tech lead establishing security practices for $ARGUMENTS. Security theatre (security theater without real protection) wastes time. Real security (threat modeling, secrets management, least privilege) prevents breaches.

## Domain Context

- **Shifting left on security** — finding vulnerabilities in development (via linters, code review) is faster than finding them in production. Bake security into process.
- **Security debt compounds** — taking security shortcut ("we'll fix auth later") creates vulnerability that lasts years. Fix upfront.
- **Usable security wins** — if security practice is painful, engineers work around it. Make it easy (password manager integrated, secrets in environment vars).
- **Threat modeling drives priorities** — not all security is equal. Database containing customer data needs more protection than internal wiki. Model threats, protect high-risk systems.

## Instructions

1. **Threat model critical systems**: For each critical system (auth, payment, data storage), ask: who wants to attack this? What are they after? What could go wrong? Prioritize protections by threat likelihood and impact.

2. **Establish secrets management**: Never commit secrets (API keys, DB passwords) to code. Use env vars (development) or secrets vault (production). Rotate secrets regularly.

3. **Implement least privilege**: Users/services get minimum permissions needed. Database user for API has read-only on necessary tables, not full admin. Reduces blast radius of compromise.

4. **Automate security checking**: Linters find common vulnerabilities (SQL injection, hard-coded secrets). Dependency scanners find vulnerable libraries. CI blocks merges on findings. Automated > manual checking.

5. **Incident response plan**: If breach happens, who escalates? Who notifies? What data was potentially exposed? Document before crisis. Practice quarterly.

## Anti-Patterns

- **Security theatre**: "We require 20-character passwords with special characters." Sounds secure but doesn't actually prevent breaches. Real security is systems-based (2FA, short-lived tokens), not password rules.
- **All-or-nothing security**: "Everything is critical, protect equally." Wastes effort. Threat-model, prioritize. Protect payment system extremely, internal wiki adequately.
- **Painful security bypassed**: "SSH key needed for deploy, takes 10 minutes to setup." Engineers write it down in Slack to avoid setup. Pain defeated security. Make security easy.
- **Secrets in code**: Committed API keys, database passwords in logs. Huge vulnerability. Use secrets vault, never commit secrets.
- **No incident response plan**: Breach happens, panic. "What do we do? Who do we notify?" Chaos. Plan before crisis. Practice quarterly (tabletop exercises).

## Further Reading

- "OWASP Top 10" — common web vulnerabilities
- "Threat Modeling" (Adam Shostack) — security-first design
- "Security Engineering" (Ross Anderson) — comprehensive security principles
- "Secrets Management" (NIST guidelines) — handling sensitive data
