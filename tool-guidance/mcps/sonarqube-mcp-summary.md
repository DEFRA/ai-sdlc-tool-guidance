# SonarQube MCP Server: Analysis for UK Government Adoption

## Tool Overview

The **SonarQube MCP Server** is a middleware application that integrates static code analysis into AI-assisted development workflows. It uses the **Model Context Protocol (MCP)**, an open standard that allows Large Language Models (LLMs)—such as those in VS Code, Cursor, or GitHub Copilot—to interact directly with a SonarQube instance.

Traditionally, developers had to manually check SonarQube dashboards. This tool allows the AI to query code quality data, retrieve rule documentation, and suggest fixes in real-time. For the UK Government, this supports 'shifting left'—addressing security and quality issues earlier in the software development lifecycle.

The tool is distributed as a Docker container (`mcp/sonarqube`) and supports two primary connection methods:

* **Stdio Transport (Local):** The AI client launches the container locally. This is the most secure method as it uses internal system pipes and avoids network exposure.
* **HTTP/HTTPS Transport (Remote):** The server runs as a persistent service over a network. This is not recommended for most government use cases unless strictly controlled via TLS.

## Privacy Settings

Privacy controls are currently limited and require manual configuration to meet government data-handling standards.

### Telemetry

By default, the server sends anonymous usage statistics to SonarSource. In government environments—particularly those handling **OFFICIAL-SENSITIVE** data—this must be disabled.

* **Required Action:** Set the environment variable `TELEMETRY_DISABLED=true`.

### Code Privacy

The server acts as a 'passthrough'. When an AI agent requests a code analysis, the code snippet is sent via the MCP server to the SonarQube backend. The MCP server does not automatically redact Personally Identifiable Information (PII) or secrets. Privacy depends entirely on whether you use a self-hosted SonarQube instance or the cloud-based SaaS version.

## Key Risks & Threat Vectors

The integration of autonomous AI agents with internal code repositories introduces four significant risks:

1. **Data Exfiltration:** The tool includes a function called `get_raw_source`. If a developer uses a public cloud AI (like standard ChatGPT or Claude), invoking this tool could send raw government source code to external servers.
2. **Prompt Injection:** A malicious actor could hide 'instructions' in a code comment. If an AI agent reads that comment via the MCP server, it could be tricked into marking a real vulnerability as a 'False Positive' in the SonarQube database.
3. **Credential Exposure:** The tool does not currently support OAuth 2.0. Users must use long-lived API tokens. If these tokens are stored in configuration files (like `mcp.json`) and accidentally committed to a repository, they provide persistent access to the organisation's code metrics.
4. **Supply Chain Risks:** There are unofficial versions of this tool (e.g., `sapientpants/sonarqube-mcp-server`) that are archived and unsupported. Only the official **SonarSource** image should be used.

## Terms of Use and Privacy Policy

* **Licensing:** The software is licensed under the **SONAR Source-Available License v1.0 (SSAL)**. This is not a standard open-source licence. While it allows internal government use, it prohibits using the tool to create a competing commercial service.
* **Privacy Policy:** Use of the tool is governed by the SonarSource Privacy Notice. If using the cloud version, data is shared with third-party processors like AWS for hosting and Braintree for billing.

## Data Management

### Multi-Regional Processing

* **SonarQube Cloud (SaaS):** Data is primarily hosted in **Frankfurt, Germany (AWS eu-central-1)**, with backups in **Ireland**. While covered by UK-EU data adequacy, some departments may require UK-only residency.
* **SonarQube Server (Self-Hosted):** This is the **recommended approach** for the UK Government, as it allows data to be kept within sovereign UK data centres or departmental cloud environments.

### Data in Transit

All communication between the MCP server and the SonarQube backend must use **HTTPS**. In local `stdio` mode, data between the IDE and the MCP server does not touch the network, which is the most secure configuration.

> **Note:** If your department uses 'break-and-inspect' TLS proxies, you must manually install your internal Root CA certificate into the Docker container to prevent connection failures.

### Data at Rest

The MCP server is 'stateless'—it does not store code or analysis results. However, it does produce logs. If the log level is set to `DEBUG`, these logs may contain sensitive code fragments or tokens.

* **Requirement:** Ensure `LOG_LEVEL` is set to `INFO` or `WARN` in production.

## Auditing

Effective auditing is difficult if teams share credentials.

* **The Attribution Problem:** If multiple developers share one 'Service Account' token, the SonarQube audit logs will show the bot performed the action, not the human who triggered the AI.
* **Requirement:** To comply with NCSC auditing principles, every developer should use their own **Personal User Token**. This ensures a clear audit trail of who is using AI to query or modify code data.

## Access Controls

The tool uses **Discretionary Access Control (DAC)**. It can only do what the user's API token allows.

* **Principle of Least Privilege:** Tokens should be restricted to 'Browse' and 'See Source Code' permissions.
* **Limitation:** There is no way to disable specific functions (like the ability to change an issue status) within the MCP server itself. Access must be managed by restricting the permissions of the user account associated with the token in the SonarQube backend.

## Compliance & Regulatory Considerations

| Standard | Status | Government Context |
| --- | --- | --- |
| **ISO 27001 / SOC 2** | Compliant | The vendor meets international security management standards. |
| **UK GDPR / DPA 2018** | Compliant | Standard Contractual Clauses (SCCs) are available for data transfers. |
| **NCSC Cloud Principles** | Partial | Alignment depends on choosing the Self-Hosted version for sensitive data. |

## References

1. [SonarSource Official MCP Documentation](https://docs.sonarsource.com/sonarqube-mcp-server)
2. [Official GitHub Repository (Source Code)](https://github.com/SonarSource/sonarqube-mcp-server)
3. [SonarSource Trust Center & Compliance](https://www.sonarsource.com/trust-center/)
4. [NCSC Guidance: Using AI in Software Development](https://www.google.com/search?q=https://www.ncsc.gov.uk/guidance/ai-and-cyber-security-principles)