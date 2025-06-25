# Cursor - Summary

**Approval status:** Approved - you can use this tool within Defra when you follow the tool guidance advice.

This summary covers the key points from the [detailed guide](cursor-detailed.md). Use it to understand how Cursor can work in government environments.

## What Cursor does

Cursor is an AI-enhanced code editor available at [cursor.com](https://www.cursor.com/). It helps developers write and refactor code more efficiently by providing AI suggestions and assistance.

The service has different tiers:
- **Free "Hobby":** Basic access for individual developers
- **Pro:** Enhanced features for individual developers
- **Business:** For organisations with team-focused features
- **Enterprise:** For large organisations with advanced security and management capabilities

## Privacy controls

Cursor now offers three distinct privacy stances:

- **Privacy Mode (Legacy):** Keeps all of your code off Cursor's servers - zero data retention or storage
- **Privacy Mode:** Still enforces zero-retention at model providers but allows encrypted, narrowly-scoped code storage so features like Background Agents and Memories can run  
- **Standard (privacy-off):** Permits broad telemetry and longer code retention for product improvement

**For UK government environments:**
- **Legacy mode** is the safest baseline - no code stored on Cursor's servers at all
- **Privacy Mode** may be acceptable with risk assessment where advanced features (Background Agents, Memories) provide clear business benefit that outweighs the limited additional data exposure
- **Standard mode** should not be used for government work due to broad data collection

**Automatic enforcement:**
- Business and Enterprise accounts automatically enforce Privacy Mode (not Legacy) by default
- Free and Pro users must manually select their preferred privacy stance
- Individual settings cannot override organisational defaults on Business/Enterprise plans

## Terms and data ownership

**Data handling and Privacy Mode:**  
The Privacy Policy (updated 8 November 2024) explains how personal data is collected and processed. With Privacy Mode (Legacy) enabled, no code is stored anywhere. With Privacy Mode enabled, code is never stored or used for training by model providers, but encrypted, narrowly-scoped code storage may occur on Cursor's servers to enable advanced features. With privacy off, some data (like code snippets and prompts) may be kept for telemetry and model improvement.

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

With Privacy Mode (Legacy) enabled, no data is stored permanently - everything is processed only in temporary memory or short-term encrypted caches and discarded immediately after processing.

With Privacy Mode enabled, encrypted, narrowly-scoped code storage may occur to enable advanced features like Background Agents and Memories, but zero-retention agreements ensure model providers do not store your code.

With privacy off, broader code data may be stored for telemetry and product improvement.

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
