# Azure Model Context Protocol (MCP) Server

## Tool Overview

The Azure Model Context Protocol (MCP) Server is a protocol implementation that acts as a secure bridge between Artificial Intelligence (AI) agents—such as GitHub Copilot or Claude—and the Azure cloud ecosystem.

Historically, connecting AI to cloud data required bespoke, hard-coded integrations. The MCP standardises this, allowing an AI "Host" to discover and use "Tools" (such as listing virtual machines or reading logs) through a universal interface. For the UK government, this enables "agentic workflows" where staff can manage infrastructure using natural language intents rather than manual CLI commands.

The server is currently in **Public Preview**. It has recently migrated from the archived `Azure/azure-mcp` repository to the central `microsoft/mcp` repository. This migration is critical because it removed the vulnerable Server-Sent Events (SSE) transport mechanism in favour of more secure standards.

## Privacy Settings

The MCP Server functions as a stateless intermediary. It does not store user data or conversation history locally.

* **Identity Integration:** It relies entirely on **Microsoft Entra ID**. It does not maintain its own user database.
* **Telemetry:** By default, the tool may send performance metadata (latency, error rates) to Microsoft under the standard Azure Privacy Statement.
* **Data Leakage Prevention:** The primary privacy risk lies in the **Host Application** (the AI chat interface). Departments must ensure the Host is configured to use Azure OpenAI or Enterprise Copilot instances to prevent government data from being used to train public foundational models.

## Key Risks & Threat Vectors

The shift to agentic infrastructure management introduces specific high-impact risks:

* **The "Confused Deputy" Problem:** This is the most significant risk. An AI agent might be tricked by a malicious prompt hidden in a document or log file (Indirect Prompt Injection). For example, an agent reading a support ticket might encounter a hidden command to "delete all storage accounts," which it then attempts to execute via the MCP Server.
* **Supply Chain Attacks:** As the tool is distributed via public registries like npm (`@azure/mcp`), there is a risk of "typosquatting," where attackers publish malicious packages with similar names.
* **Privilege Escalation:** If a user with high-level permissions (e.g., "Owner") uses the MCP Server, the AI agent inherits those full permissions. There is no built-in "step-down" mechanism within the protocol itself.

## Terms of Use and Privacy Policy

* **Licensing:** The software is provided under the **MIT License**. This is a permissive license but includes a total disclaimer of warranty.
* **Preview Status:** As a Public Preview tool, it is provided "as-is" without a Service Level Agreement (SLA). It is not currently recommended for Critical National Infrastructure (CNI) or production-grade "OFFICIAL-SENSITIVE" systems without extensive compensating controls.
* **Liability:** Under the Supplemental Terms for Azure Previews, Microsoft is not liable for damages arising from the use of the tool.

## Data Management

### Multi-Regional Processing

The MCP Server is a portable software component. To ensure data sovereignty, UK government departments should host the server within the **UK South (London)** or **UK West (Cardiff)** regions. This ensures the logic and data processing remain within the UK legal jurisdiction.

### Data in Transit

All communications between the MCP Server and the Azure Resource Manager (ARM) API are encrypted using **TLS 1.2 or higher**. If the server is deployed locally, it uses `stdio` (standard input/output), meaning the data never leaves the local machine's memory.

### Data at Rest

The MCP Server is stateless and does not persist data. However, it interacts with data stored at rest in Azure (e.g., Storage Accounts). These backend services use **AES-256 encryption** by default. For higher assurance, departments should use **Customer-Managed Keys (CMK)** to maintain control over the data's cryptographic lifecycle.

## Auditing

The default logging for the MCP Server is insufficient for government standards, as logs are often only sent to a local terminal.

To meet NCSC Principle 13 (Audit Information), departments must implement a **Gateway Pattern**. By placing the MCP Server behind an Azure API Management (APIM) gateway, every "Tool Call" made by the AI can be logged to a central **Azure Sentinel** workspace.

| Audit Requirement | Default Status | Required Configuration |
| --- | --- | --- |
| **Identity Attribution** | Partial | Link Entra ID OID to every request |
| **Command Logging** | No | Log JSON-RPC request/response bodies |
| **Centralised Storage** | No | Stream logs to Azure Monitor/Sentinel |

## Access Controls

Access is governed by the **Principle of Least Privilege**:

* **Role-Based Access Control (RBAC):** Users should be assigned "Custom Roles" that limit the tools the AI can use (e.g., allowing "Read" but denying "Delete").
* **Conditional Access:** Access should be restricted to managed, compliant devices originating from UK IP addresses.
* **Privileged Identity Management (PIM):** For any "Write" or "Delete" actions, users should be required to activate Just-In-Time (JIT) access, ensuring permissions are not "always on."

## Compliance & Regulatory Considerations

* **G-Cloud:** The underlying Azure services are accredited for OFFICIAL and OFFICIAL-SENSITIVE data.
* **NCSC Cloud Security Principles:** The tool aligns well with transit and asset protection principles but requires custom engineering to meet auditing and governance requirements.
* **GDPR:** The department remains the Data Controller. You must ensure the AI agent does not process Personal Identifiable Information (PII) in a way that violates the Data Protection Act 2018.

## References

1. **Active Source Code:** [Microsoft MCP GitHub Repository](https://github.com/microsoft/mcp) (Replaced `Azure/azure-mcp` in Sept 2025).
2. **Protocol Specification:** Model Context Protocol (MCP) Official Documentation.
3. **Security Guidance:** NCSC Cloud Security Principles and Microsoft Azure Security Benchmarks.
4. **Licensing:** MIT License Agreement and Supplemental Terms for Microsoft Azure Previews.