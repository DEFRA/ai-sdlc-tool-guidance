# Atlassian Rovo (Remote) MCP Server

## Tool Overview

The Atlassian Model Context Protocol (MCP) server is an open-standard connector. It allows Artificial Intelligence (AI) models—such as Anthropic’s Claude, OpenAI’s GPT-4, or coding assistants like Cursor—to securely access and interact with data stored within Atlassian products (Jira, Confluence, and Compass).

There are two primary ways to implement this:

1. **Official Atlassian Rovo (Remote) MCP Server:** A vendor-managed Cloud service using an OAuth 2.1 framework.
2. **Community-Developed Servers:** Self-hosted versions (typically via Docker) that support both Cloud and "Data Center" (on-premise) installations.

The tool enables "agentic workflows," where an AI can proactively search for Jira tickets, read Confluence pages, and create new content based on user instructions, rather than simply generating text in isolation.

## Privacy Settings

Privacy is governed by the **Principle of Least Privilege**. The AI agent does not have its own "admin" access; instead, it operates entirely within the context of the authenticated user.

* **User-Scoped Access:** The AI can only see or modify data that the specific human user is already authorised to access.
* **Granular Scopes:** During the initial setup, users must approve specific "scopes" (e.g., "Read Jira issues" or "Write Confluence pages").
* **Application-Level Control:** Administrators can allowlist or block specific external domains from connecting to their Atlassian environment via MCP settings in the Atlassian Administration portal.

## Key Risks & Threat Vectors

* **Supply Chain Attacks ("The Rug Pull"):** Since many users run the connector using `npx` (which fetches the latest code version), a malicious actor could theoretically update a community package to exfiltrate data.
* **Data Sovereignty & Routing:** The official server routes requests through a global endpoint (`mcp.atlassian.com`). For UK organisations with strict data residency requirements, this transit through non-UK infrastructure may pose a compliance risk.
* **Static Credential Leakage:** Community-hosted versions often use API Tokens or Personal Access Tokens (PATs). If these tokens are not managed in a secure vault, they provide persistent access to the data estate.
* **AI Hallucination in "Write" Operations:** While rare, an AI agent could incorrectly interpret a prompt and create multiple redundant Jira tickets or Confluence pages, leading to "data noise."

## Terms of Use and Privacy Policy

The official MCP server is currently in **Public Beta**. Use is governed by the standard Atlassian Cloud Terms of Service and the specific Beta Product Addendum.

* **No "Delete" Capability:** To mitigate risk, the official tool generally does not support the deletion of data.
* **Beta Liability:** As a beta product, it does not currently carry the same Service Level Agreements (SLAs) or support guarantees as General Availability (GA) products.

## Data Management

### Multi-Regional Processing

The official Atlassian MCP server acts as a global gateway. Even if your Jira data is "at rest" in the UK (London region), requests made through the official MCP endpoint are processed via Atlassian’s global infrastructure, which may involve transient processing in the United States.

### Data in Transit

All data moving between the AI Host (e.g., Claude Desktop) and the Atlassian Server is encrypted using **TLS 1.2+**. The official server uses **Server-Sent Events (SSE)** for streaming, ensuring a secure, unidirectional flow of information from the server to the client.

### Data at Rest

The MCP server itself is a "stateless" connector; it does not store your Jira or Confluence data. It merely facilitates the conversation between the AI and the database. However, the underlying data remains stored in the customer's Atlassian Cloud instance, which adheres to Atlassian's standard data residency and encryption-at-rest protocols.

## Auditing

Monitoring AI activity is critical for enterprise governance:

* **Atlassian Guard Premium:** Organisations should use Guard Premium to access **Tool Invocation Logs**. This identifies exactly which AI tool was used and when.
* **Standard API Logs:** Without Guard Premium, activity appears as standard API requests, making it difficult to distinguish between a human action and an AI agent action.

## Access Controls

Access is managed through two layers:

1. **Identity Provider (IdP) Authentication:** Users must log in via the organisation's standard SSO (e.g., Okta or Azure AD) to initiate the OAuth flow.
2. **Site-Level Permissions:** Even with a valid token, the MCP server respects all internal Jira/Confluence permissions, including "Issue Security Levels" and "Page Restrictions."

## Compliance & Regulatory Considerations

* **GDPR / UK Data Protection Act:** Organisations must assess whether the global routing of the official server constitutes a "restricted transfer" of personal data.
* **UK Official Sensitive:** For high-security environments, the **Self-Hosted Community Model** is recommended. This allows the MCP server to reside within a UK-sovereign Virtual Private Cloud (VPC), ensuring data never leaves the approved jurisdictional boundary.

---

### Comparison of Deployment Models

| Feature | Official (SaaS) | Community (Self-Hosted) |
| --- | --- | --- |
| **Best For** | Fast setup, Cloud users | Data sovereignty, On-premise |
| **Maintenance** | Managed by Atlassian | Managed by your IT team |
| **UK Data Residency** | Transits global endpoints | Can be locked to UK regions |
| **Authentication** | OAuth 2.1 (Interactive) | API Tokens / PATs (Static) |

---

## References

1. Atlassian Rovo Documentation (2025).
2. Model Context Protocol (MCP) Specification, Anthropic PBC.
3. Atlassian Trust Centre: Data Residency and Privacy.
4. "Sooperset" Open Source MCP Repository (GitHub).