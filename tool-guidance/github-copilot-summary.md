# GitHub Copilot for Business - Summary

This summary covers the key points from the [detailed guide](github-copilot-detailed.md). Use it to understand how GitHub Copilot can work in government environments.

## What GitHub Copilot does
GitHub Copilot for Business is an AI‑powered coding assistant that works with common code editors and the GitHub platform. It predicts and suggests code based on natural language prompts and surrounding context. This aims to improve developer productivity and code quality. The Business tier adds seat‑based licensing, centralised admin controls and enterprise‑grade privacy safeguards.

## Privacy controls
- **Public code filtering** – stops suggestions that closely match public GitHub code  
- **Content exclusions** – lets admins exclude specific paths so they are never referenced in prompts or suggestions  
- **No retention of prompts or completions** – the Business plan turns off data‑collection for model training by default  
- **Choice of AI model** – organisations can turn off third‑party models, keeping all processing on Microsoft/GitHub infrastructure  
- **Organisation‑wide enforcement** – privacy settings are set once and cannot be overridden by individual users

## Terms and data ownership
GitHub's Terms for Copilot and the GitHub Privacy Statement apply. The Business plan contractually confirms that:
- customer code, prompts and completions are **not** used for model training  
- data protection is provided under the Microsoft Online Services Data Protection Addendum (DPA)  
- international transfers rely on the EU‑US Data Privacy Framework and Standard Contractual Clauses

## Where your data goes

### Data processing locations
Inference requests are routed through Microsoft‑owned infrastructure. Primary processing happens in EU and US Azure regions. Organisations cannot yet mandate UK‑only processing.

### Data protection in transit
All traffic uses TLS 1.2+ encryption. Requests sent to the model back‑end are proxied through GitHub so developer IPs are not exposed downstream.

### Data protection at rest
Minimal telemetry (time‑stamped hashes, seat identifiers) is stored in encrypted Azure SQL and Log Analytics. Source code, prompts and completions are discarded once the response is returned.

## Audit logs
GitHub keeps operational logs (7–30 days) containing telemetry but **never raw code**. Admins can export aggregated usage reports via the GitHub REST API.

## Access controls
- GitHub SSO / SAML 2.0 integration with conditional access  
- Role‑based access (organisation owner, security manager, billing manager)  
- Just‑in‑time privileged access for GitHub staff with full audit trail

## Compliance and regulation
- SOC 2 Type II, ISO 27001/27018 and CSA STAR certifications cover the underlying GitHub platform  
- Copilot aligns with GDPR principles and the UK GDPR - no code is kept beyond temporary processing  
- Not yet suitable for "OFFICIAL‑SENSITIVE" or above unless a departmental risk assessment is completed

## What to do next

1. Review the [detailed guide](github-copilot-detailed.md) for technical specifications
2. Check if EU and US data processing meets your data residency requirements
3. Assess whether the privacy controls meet your departmental policies
4. Consider if the compliance certifications align with your needs

## References

- [GitHub Copilot for Business](https://github.com/features/copilot#copilot-for-business)  
- [GitHub Docs – "What is GitHub Copilot?"](https://docs.github.com/en/copilot/overview-of-github-copilot)  
- [GitHub Blog – Copilot for Business announcement](https://github.blog/2023-02-14-introducing-github-copilot-for-business/)  
- [Microsoft Online Services Data Protection Agreement](https://learn.microsoft.com/legal/gdpr)  
- [GitHub Trust Center](https://trust.github.com/)

