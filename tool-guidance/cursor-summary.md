# Cursor - Summary

This summary covers the key points from the [detailed guide](cursor-detailed.md). Use it to understand how Cursor can work in government environments.

## What Cursor does

Cursor is an AI-enhanced code editor available at [cursor.com](https://www.cursor.com/). It helps developers write and refactor code more efficiently by providing AI suggestions and assistance.

The service has different tiers:
- **Free "Hobby":** Basic access for individual developers
- **Pro:** Enhanced features for individual developers
- **Business:** For organisations with team-focused features
- **Enterprise:** For large organisations with advanced security and management capabilities

## Privacy controls

Cursor provides strong privacy controls:
- **Privacy Mode:** Ensures your source code and prompts are never stored or used for training
- **Data processing:** When Privacy Mode is enabled, data stays only in temporary memory or short-term encrypted caches
- **Automatic enforcement:** Privacy Mode is automatically enforced for Business and Enterprise accounts
- **Manual activation:** Free and Pro users must enable Privacy Mode manually

## Terms and data ownership

**Data handling and Privacy Mode:**  
The Privacy Policy (updated 8 November 2024) explains how personal data is collected and processed. With Privacy Mode enabled, code is never stored or used for training. With Privacy Mode off, some data (like code snippets and prompts) may be kept for telemetry and model improvement.

**International data transfers:**  
The policy states that data is processed on US-based servers. For UK/EU users, Standard Contractual Clauses or equivalent safeguards protect international transfers.

**GDPR compliance:**  
Cursor's practices emphasise data minimisation, user rights (such as account deletion), and overall GDPR compliance. However, UK government users should review these policies closely to make sure they meet specific departmental requirements.

## Where your data goes

### Data processing locations

Although a UK user's requests may first reach a London AWS data centre for low latency, most processing happens on US-based infrastructure (with some parts also on Azure and Google Cloud). Custom AI models, hosted via Fireworks, might run in the US, Europe, or Asia.

Even if you configure your own API keys, all requests still route through Cursor's backend.
  
### Data protection in transit  

Data is protected in transit using TLS 1.2. Any code that is stored uses AES-256 encryption. Minimal retention is practised, as code is primarily processed in memory.

### Data protection at rest

Cursor may store vector embeddings and metadata (not raw source code) for features like codebase indexing. This ensures that searchable artifacts cannot be reversed to reveal original content.

When privacy mode is enabled, no data is stored permanently. Data stays only in temporary memory or short-term encrypted caches and is discarded immediately after processing.

### Third-party processing  

Code data may be sent to US-based AI model providers (such as OpenAI and Anthropic) under zero data retention agreements. This ensures your data is not stored beyond immediate processing.

## Audit logs

Cursor's logging practices, especially for privacy-mode requests, avoid capturing sensitive code details.

## Access controls

Cursor applies least-privilege and multi-factor authentication for internal access.

For enterprise users, an admin dashboard provides aggregated usage metrics (for example, number of queries and completions) without keeping the content of your code.

Cursor integrates with enterprise identity systems (SSO with SAML 2.0/OIDC) and enforces role-based access. Even if individual settings could be adjusted locally, the backend defaults ensure Privacy Mode is maintained.

## Compliance and regulation

**GDPR and data minimisation**  
Cursor's policies align with GDPR principles - emphasising data minimisation and providing user rights such as data deletion. However, UK government users must note that data is ultimately processed in the US (or other jurisdictions) under mechanisms such as Standard Contractual Clauses.

**Certifications and assurance**  
Cursor is SOC 2 Type II certified, showing its commitment to security and operational best practices. However, it does not offer a UK-sovereign cloud option.

## What to do next

1. Review the [detailed guide](cursor-detailed.md) for technical specifications
2. Decide if US data processing is acceptable for your use case
3. Check if Privacy Mode meets your data protection requirements
4. Consider whether SOC 2 Type II certification meets your compliance needs

## References

- [Security](https://www.cursor.com/security)
- [Enterprise](https://www.cursor.com/enterprise)
- [Privacy Policy](https://www.cursor.com/privacy)
- [Pricing](https://www.cursor.com/pricing)
- [Do the Cursor Policies comply with GDPR fully?](https://forum.cursor.com/t/do-the-cursor-policies-comply-with-gdpr-fully/20294)
