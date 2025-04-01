# Cursor - Summary Guidance

This is a high-level summary of the [detailed report](cursor-detailed.md)

## 1. Tool Overview

Cursor is an AI-augmented code editor (available at [cursor.com](https://www.cursor.com/)) designed to help developers write and refactor code more efficiently. 

The service is offered in several tiers:
- **Free "Hobby":** Basic access for individual developers
- **Pro:** Enhanced features for individual developers
- **Business:** Designed for organisations with team-focused features
- **Enterprise:** Tailored for large organisations with advanced security and management capabilities

## 2. Privacy Settings

Cursor provides robust privacy controls:
- **Privacy Mode:** Ensures source code and prompts are never stored or used for training
- **Data Processing:** When Privacy Mode is enabled, data remains only in transient memory or short-term encrypted caches
- **Automatic Enforcement:** Privacy Mode is automatically enforced for Business and Enterprise accounts
- **Manual Activation:** Free and Pro users must enable Privacy Mode manually

## 3. Terms of Use and Privacy Policy

**Data Handling & Privacy Mode:**  
The Privacy Policy, last updated on 8 November 2024, details how personal data is collected and processed. With Privacy Mode enabled, code is never stored or used for training. With Privacy Mode off, some data (like code snippets and prompts) may be retained for telemetry and model improvement.

**International Data Transfers:**  
The policy explicitly states that data is processed on US-based servers, and for UK/EU users, Standard Contractual Clauses or equivalent safeguards are used for international transfers.

**GDPR Compliance:**  
Cursor's practices emphasise data minimisation, user rights (such as account deletion), and overall compliance with GDPR principles. However, UK government users should review these policies closely to ensure they meet specific departmental requirements.

## 4. Data Management

### 4.1 Multi-Regional Processing

Although a UK user's requests may first reach a London AWS data centre for low latency, most processing occurs on US-based infrastructure (with some parts also on Azure and Google Cloud). Custom AI models, hosted via Fireworks, might run in the US, Europe, or Asia.

Even if you configure your own API keys, all requests will still route through Cursor's backend.
  
### 4.2 Data in Transit  

Data is protected in transit using TLS 1.2, and any code that is stored is encrypted with AES-256. Minimal retention is practiced, as code is primarily processed in memory.

### 4.3 Data at Rest

Cursor may store vector embeddings and metadata (not raw source code) for features like codebase indexing, ensuring that searchable artifacts can't be reversed to reveal original content.

When privacy mode is enabled no data is stored persistently. Data remains only in transient memory or short-term encrypted caches and is discarded immediately after processing.

### 4.4 Third-Party Processing  

Code data may be sent to US-based AI model providers (such as OpenAI and Anthropic) under zero data retention agreements, ensuring that your data is not stored beyond immediate processing.

## 5. Auditing

Its logging practices, especially for privacy-mode requests, are designed to avoid capturing sensitive code details.

## 6. Access Controls

Cursor applies least-privilege and multi-factor authentication for internal access.

For enterprise users, an admin dashboard provides aggregated usage metrics (e.g., number of queries and completions) without retaining the content of your code.

Cursor integrates with enterprise identity systems (SSO with SAML 2.0/OIDC) and enforces role-based access. Even if individual settings could be adjusted locally, the backend defaults ensure Privacy Mode is maintained.

## 7. Compliance & Regulatory Considerations

**GDPR & Data Minimisation**  
Cursor's policies align with GDPR principles—emphasising data minimisation and providing user rights such as data deletion. However, UK government users must note that data is ultimately processed in the US (or other jurisdictions) under mechanisms such as Standard Contractual Clauses.

**Certifications & Assurance**  
Cursor is SOC 2 Type II certified, underscoring its commitment to security and operational best practices, though it does not offer a UK-sovereign cloud option.

## 8. References

- [Security | Cursor - The AI Code Editor](https://www.cursor.com/security#:~:text=While%20we%20have%20several%20large,make%20a%20proper%20risk%20assessment)
- [Enterprise | Cursor - The AI Code Editor](https://www.cursor.com/enterprise#:~:text=How%20does%20Cursor%20secure%20my,code)
- [Privacy Policy | Cursor - The AI Code Editor](https://www.cursor.com/privacy#:~:text=TLDR)
- [Pricing | Cursor - The AI Code Editor](https://www.cursor.com/pricing#:~:text=Everything%20in%20Pro%2C%20plus)
- [Enterprise | Cursor - The AI Code Editor](https://www.cursor.com/enterprise#:~:text=Do%20you%20support%20SSO%3F)
- [Do the Cursor Policies comply with GDPR fully? - Cursor Community Forum](https://forum.cursor.com/t/do-the-cursor-policies-comply-with-gdpr-fully/20294#:~:text=%E2%80%A2%20Ensure%20explicit%2C%20informed%20consent,when%20Privacy%20Mode%20is%20off)
