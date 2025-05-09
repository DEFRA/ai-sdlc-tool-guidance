# GitHub Copilot for Business

## Tool Overview
GitHub Copilot for Business is an AI‑powered coding assistant that integrates with common IDEs and the GitHub platform. It predicts and inserts code based on natural language prompts and surrounding context, aiming to improve developer productivity and code quality. The Business tier adds seat‑based licensing, centralised admin controls and enterprise‑grade privacy safeguards.

## Privacy Settings
- **Public code filtering** – suppresses suggestions that closely match public GitHub code.  
- **Content exclusions** – lets admins exclude specific paths so they are never referenced in prompts or suggestions.  
- **No retention of prompts or completions** – the Business plan disables data‑collection for model training by default.  
- **Choice of AI model** – organisations can disable third‑party models, keeping all processing on Microsoft/GitHub infrastructure.  
- **Org‑wide enforcement** – privacy settings are set once and can’t be overridden by individual users.

## Terms of Use and Privacy Policy
GitHub’s Terms for Copilot and the GitHub Privacy Statement apply. The Business plan contractually confirms that:
- customer code, prompts and completions are **not** used for model training;  
- data protection is provided under the Microsoft Online Services Data Protection Addendum (DPA);  
- international transfers rely on the EU‑US Data Privacy Framework and Standard Contractual Clauses.

## Data Management

### Multi‑Regional Processing
Inference requests are routed through Microsoft‑owned infrastructure. Primary processing happens in EU and US Azure regions; organisations cannot yet mandate UK‑only processing.

### Data in Transit
All traffic is encrypted with TLS 1.2+. Requests sent to the model back‑end are proxied through GitHub so developer IPs are not exposed downstream.

### Data at Rest
Minimal telemetry (time‑stamped hashes, seat identifiers) is stored in encrypted Azure SQL and Log Analytics. Source code, prompts and completions are discarded once the response is returned.

## Auditing
GitHub retains operational logs (7–30 days) containing telemetry but **never raw code**. Admins can export aggregated usage reports via the GitHub REST API.

## Access Controls
- GitHub SSO / SAML 2.0 integration with conditional access.  
- Role‑based access (org owner, security manager, billing manager).  
- Just‑in‑time privileged access for GitHub staff with full audit trail.

## Compliance & Regulatory Considerations
- SOC 2 Type II, ISO 27001/27018 and CSA STAR certifications cover the underlying GitHub platform.  
- Copilot aligns with GDPR principles and the UK GDPR; no code is kept beyond transient processing.  
- Not yet suitable for “OFFICIAL‑SENSITIVE” or above unless a departmental risk assessment is completed.

## References

- [GitHub Copilot for Business](https://github.com/features/copilot#copilot-for-business)  
- [GitHub Docs – “What is GitHub Copilot?”](https://docs.github.com/en/copilot/overview-of-github-copilot)  
- [GitHub Blog – Copilot for Business announcement](https://github.blog/2023-02-14-introducing-github-copilot-for-business/)  
- [Microsoft Online Services Data Protection Addendum](https://learn.microsoft.com/legal/gdpr)  
- [GitHub Trust Center](https://trust.github.com/)

