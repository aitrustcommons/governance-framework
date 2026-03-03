# AI Trust Commons — Governance Framework

**Cross-provider governance and compliance for AI agents in the enterprise.**

AI agents are proliferating faster than any prior technology category. 80% of Fortune 500 companies now deploy active AI agents — but only 14.4% report that all agents go live with full security and IT approval. 88% have experienced confirmed or suspected agent security incidents in the past year.

The governance tools exist. The standards exist. What's missing is the connective layer that ties them together across providers, protocols, and compliance regimes — so that an enterprise deploying agents across AWS, Azure, and GCP doesn't have to independently map every security control to every compliance obligation.

**AI Trust Commons** is an open-source initiative building that layer.

---

## The Problem

Every major cloud vendor publishes AI agent governance guidance — for their own platform. Microsoft's MCP Gateway handles routing and auth within Azure. Google's Agent Builder Console governs agents on Vertex AI. AWS Bedrock has its own guardrails. Each solves a real problem. None addresses what happens at the seams.

Meanwhile, enterprises must simultaneously satisfy overlapping and disconnected standards:

- **Agent protocols:** MCP, A2A, ACP
- **Identity & auth:** OAuth 2.1, OpenID Connect, SPIFFE/SPIRE, SCIM
- **Threat frameworks:** OWASP Top 10 for Agentic Applications, MITRE ATLAS
- **Policy engines:** Cedar, OPA/Rego, AWS Verified Permissions
- **AI governance:** NIST AI RMF, NIST AI 600-1, EU AI Act
- **Compliance regimes:** SOC 2, PCI DSS, HIPAA, COPPA/FERPA, FedRAMP

Every team maps these independently. Every team reaches different conclusions. Engineering capacity gets consumed proving the same control satisfies three different audits. And AI agents — which operate at machine speed, across cloud boundaries, with autonomous decision-making — amplify every gap.

## What This Framework Does

The AI Trust Commons Governance Framework provides:

### Standards Mapping
An authoritative crosswalk showing how controls map across frameworks — so that implementing MCP authentication with OAuth 2.1 scoped tokens gets credit across SOC 2, NIST AI RMF, and EU AI Act audits simultaneously, instead of proving the same control three different ways.

### Policy-as-Code Governance
Machine-readable compliance policies that AI agents can be validated against in real time. Compliance was designed for human-speed review of human-speed work. When AI agents generate code and take actions at machine speed, governance must operate at the same speed — as a guardrail agents run alongside, not a gate teams stop and open.

### Cross-Provider Audit Trails
A standard format for agent action logs that works across AWS, Azure, GCP, and hybrid environments. What the agent did, what data it accessed, what authorization chain it operated under, why it made each decision. Currently, most AI coding tools produce no structured record of what they changed or why — the audit trail gap that no vendor has incentive to solve for environments beyond their own platform.

### OWASP MCP Top 10 Validation
Automated validation of agent tool calls against the OWASP Top 10 for Agentic Applications — covering agent goal hijack, tool misuse, identity and privilege abuse, supply chain vulnerabilities, unexpected code execution, memory poisoning, insecure inter-agent communication, excessive agency, inadequate guardrails, and cascading failures.

## Architecture

```
┌─────────────────────────────────────────────────┐
│                 AI Agent / Client                │
└─────────────────┬───────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────┐
│          Governance Framework (Proxy)            │
│                                                  │
│  ┌──────────┐ ┌──────────┐ ┌─────────────────┐  │
│  │ Policy   │ │ OWASP    │ │ Audit Trail     │  │
│  │ Engine   │ │ Validator│ │ Generator       │  │
│  │ (Cedar)  │ │          │ │ (OpenTelemetry) │  │
│  └──────────┘ └──────────┘ └─────────────────┘  │
│                                                  │
│  ┌──────────────────────────────────────────┐    │
│  │ Compliance Mapper                        │    │
│  │ NIST AI RMF ↔ OWASP ↔ SOC 2 ↔ EU AI Act│    │
│  └──────────────────────────────────────────┘    │
└─────────────────┬───────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────┐
│          MCP Servers / Tools / APIs              │
│          (AWS, Azure, GCP, hybrid)               │
└─────────────────────────────────────────────────┘
```

The framework operates as an interceptor between AI agents and the tools they access. It enforces policies, validates actions against threat frameworks, generates compliance-ready audit logs, and maps every control to the regulatory obligations it satisfies — across providers.

## Roadmap

| Phase | Focus | Status |
|-------|-------|--------|
| **Phase 0** | Standards landscape research, NIST RFI public comment, OWASP engagement | ✅ Active |
| **Phase 1** | Compliance mapping engine — OWASP Top 10 ↔ NIST AI RMF ↔ SOC 2 ↔ EU AI Act | 🔜 Next |
| **Phase 2** | Policy-as-code engine (Cedar) with MCP interceptor proxy | Planned |
| **Phase 3** | Cross-provider audit trail generation (OpenTelemetry) | Planned |
| **Phase 4** | Reference deployment — Kubernetes, multi-cloud | Planned |

## Standards Engagement

This initiative engages directly with the standards bodies shaping AI agent governance:

- **NIST** — Public comment submitted to the CAISI Request for Information on AI Agent Security (NIST-2025-0035, March 2026). NCCoE AI Agent Identity and Authorization concept paper comment in preparation (due April 2, 2026).
- **OWASP** — Contributing to the MCP Top 10 project and the Agentic Security Initiative.
- **EU AI Act** — Framework includes Article 50 transparency record generation for high-risk AI systems (compliance deadline August 2026).

## Project Structure

```
governance-framework/
├── README.md
├── LICENSE                          # Apache 2.0
├── docs/
│   ├── architecture/                # Architecture Decision Records (ADRs)
│   ├── compliance-mappings/         # Standards crosswalk documentation
│   └── research/                    # Landscape analysis, NIST submissions
├── src/                             # Framework source code
│   ├── policy-engine/               # Cedar policy definitions & evaluation
│   ├── owasp-validator/             # OWASP Top 10 validation rules
│   ├── audit-trail/                 # OpenTelemetry-based logging
│   └── compliance-mapper/           # Cross-framework control mapping
└── tests/
```

## Why This Exists

I spent 25 years leading engineering organizations at Microsoft, AT&T, T-Mobile, Expedia Group, and Hitachi Consulting. At every one of them, I watched compliance governance fail — not because the standards were wrong, but because no single team owned the outcome, no framework mapped to any other, and every team independently reinvented the compliance wheel under delivery pressure.

AI agents compress that failure cycle. They take autonomous actions at machine speed across cloud boundaries, with no audit trail and no compliance context. The governance gap I saw take months to cause problems now takes hours.

I founded AI Trust Commons because the governance layer the industry needs — cross-provider, standards-mapped, machine-readable — is something no single vendor will build. Every vendor solves for their own platform. This project solves for the enterprise that operates across all of them.

**Nikhil Singhal**
CTO | VP Engineering | 25 years across Microsoft, AT&T, T-Mobile, Expedia, Hitachi
[LinkedIn](https://linkedin.com/in/nikhilsinghal) · [GitHub](https://github.com/nikhilsi) · [Email](mailto:nikhil@aitrustcommons.org)

## Contributing

AI Trust Commons is open to contributors. Whether you're a security engineer, compliance professional, policy researcher, or enterprise architect dealing with these problems firsthand — your perspective makes this better.

- Open an issue to discuss ideas or report gaps
- Submit a PR to improve mappings, policies, or documentation
- Share real-world compliance challenges that the framework should address

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

Apache 2.0 — see [LICENSE](LICENSE) for details.
