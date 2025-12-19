# GitHub Model Context Protocol (MCP) Server

## Tool Overview

The GitHub Model Context Protocol (MCP) Server acts as a universal bridge between Large Language Models (LLMs) and the GitHub platform. It enables AI agents to move beyond providing advice to performing active work, such as reading repositories, managing issues, and reviewing pull requests.

The tool uses an open standard that decouples the AI model from the specific tool implementation, often described as a "USB-C for AI applications". For the UK government, this represents a shift toward "Agentic AI", where software can act on behalf of a civil servant to maintain digital infrastructure.

The server can be deployed in two ways:

* **Local Deployment:** Runs on a developer’s workstation. It uses standard input/output (`stdio`) to communicate, keeping the control plane on the vetted device.
* **Remote Deployment:** A hosted service managed by GitHub that uses Server-Sent Events (SSE) for communication.

## Privacy Settings

Privacy in the MCP ecosystem is determined by how the server is authenticated and which LLM endpoint is used.

* **Authentication:** * **Remote:** Uses OAuth 2.0, allowing for centralised identity management and integration with Entra ID (Azure AD).
* **Local:** Uses Personal Access Tokens (PATs). To maintain security, departments must enforce **Fine-Grained PATs** to limit access to specific repositories rather than the entire estate.


* **Model Privacy:** The primary risk is data leakage to model providers. Use of the MCP server must be restricted to "Zero-Data Retention" environments (e.g., GitHub Copilot Enterprise or Azure OpenAI) to ensure government code is not used for model training.

## Key Risks & Threat Vectors

The transition from passive AI to active agents introduces several critical security risks:

* **Prompt Injection (The "Confused Deputy"):** An attacker could place malicious instructions in a repository (e.g., in a code comment). When an agent reads that file, it may follow the hidden instruction to perform unauthorised actions, such as merging malicious code.
* **Data Exfiltration:** If an agent has access to both the GitHub MCP server and a web browser tool, it could be tricked into reading a secret and "pasting" it to an external URL.
* **Supply Chain Attacks:** Installing the server via public registries (like `npm`) carries risks of typosquatting or dependency hijacking.
* **Resource Exhaustion:** AI "hallucinations" or logic loops could trigger thousands of API calls, leading to a Denial of Service (DoS) by exhausting GitHub API rate limits.

## Terms of Use and Privacy Policy

* **Licensing:** The software is available under the **MIT Licence**. This means HMG assumes full operational risk, as the software is provided "as is" without warranty.
* **Data Controller:** For the remote configuration, GitHub Inc. (US) acts as the data controller.
* **Service Requirements:** While the MCP server itself is open-source, using it with the Copilot Coding Agent requires a paid **GitHub Copilot Business** or **Enterprise** licence.

## Data Management

### Multi-Regional Processing

GitHub operates a global infrastructure, primarily based in the **United States**. While data residency options exist for the EU, there is currently **no UK-specific data residency region**. For highly sensitive "UK-eyes only" data, a local MCP server connected to a self-hosted GitHub Enterprise Server (GHES) within a UK data centre is the only sovereign solution.

### Data in Transit

All communications between the AI client, the MCP server, and GitHub are encrypted using **TLS 1.2 or higher**. This aligns with NCSC guidance for protecting data in transit.

### Data at Rest

The MCP server is **stateless**; it does not store repository contents on its own disk. However, the AI client (such as Visual Studio Code) may cache chat history and code snippets locally. Consequently, Full Disk Encryption is mandatory for all developer endpoints.

## Auditing

There is currently an **"Attribution Gap"** in standard logs. When an AI agent performs an action (e.g., deleting a branch), GitHub audit logs show the action as being performed by the human user. This makes it difficult to distinguish between intentional human actions and "Confused Deputy" attacks. Departments must implement client-side logging to capture the prompts and tool calls for forensic purposes.

## Access Controls

To mitigate risk, the following controls are recommended:

1. **Read-Only Mode:** This should be the default configuration. It allows agents to analyse code without the ability to modify it.
2. **Toolset Scoping:** Administrators can disable specific capabilities, such as the ability to trigger GitHub Actions (CI/CD) or access security alerts.
3. **Organisation Kill-Switch:** Administrators can use GitHub Enterprise policies to disable all MCP server integrations across the organisation if a threat is detected.

## Compliance & Regulatory Considerations

* **NCSC Principles:** Deployment must align with the NCSC's pillars for secure AI development, specifically focusing on human-in-the-loop verification for code changes.
* **UK GDPR:** A Data Protection Impact Assessment (DPIA) is required. Particular attention must be paid to Article 22, ensuring that no significant actions (like merging code to production) are handled by a solely automated process.
* **GovS 007:** To meet government security standards, departments must move away from "Classic" PATs and ensure all binaries are scanned and hosted in internal artifact repositories.

---

## References

* [GitHub MCP Server Repository](https://github.com/github/github-mcp-server)
* [NCSC Guidelines for Secure AI System Development](https://www.ncsc.gov.uk/collection/guidelines-secure-ai-system-development)
* [Model Context Protocol Specification](https://modelcontextprotocol.io/)
* [OWASP LLM01: Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)