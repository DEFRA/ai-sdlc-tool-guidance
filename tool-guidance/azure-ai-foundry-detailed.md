# Azure AI Foundry - Detailed Guide

**Approval status:** Approved - you can use this tool within Defra when you follow the tool guidance advice.

*(Generated by AI, ChatGPT Deep Research, on April 25th June 2025)*

## 1. Tool Overview
Azure AI Foundry is Microsoft's managed platform for designing, building and running generative AI applications at scale.  
It brings together **model catalogues**, **multi-agent toolchains**, managed compute and governance capabilities in a single portal, SDK and REST API.[^1]

Key use cases include:
- Evaluating and deploying foundation, open-source and domain models
- Fine-tuning and safeguarding models with responsible AI tooling
- Orchestrating multi-step "agent" workflows
- Governing AI projects through hubs, projects and central policy controls

Website: <https://learn.microsoft.com/en-gb/azure/ai-foundry/>

## 2. Privacy Settings
- **Private networking** – you can create hubs and projects inside a managed virtual network and access them exclusively through Azure Private Link, blocking public internet traffic.[^2]  
- **Customer-managed keys (CMK)** – administrators can encrypt metadata and artefacts with keys held in Azure Key Vault.[^2]  
- **Conditional Access and RBAC** – Microsoft Entra Conditional Access policies and Azure RBAC (role-based access control) roles restrict who can view or edit resources.[^3]  
- **Optional diagnostic data** – administrators choose whether to stream resource logs to Log Analytics; no telemetry is enforced.[^4]

## 3. Terms of Use and Privacy Policy
| Document | Purpose | Link |
|----------|---------|------|
| Microsoft Product Terms | Governs use of all Azure services, including AI Foundry | <https://www.microsoft.com/licensing/terms> |
| Microsoft Products & Services Data Protection Addendum | Contractual GDPR compliance and data-processing terms | <https://aka.ms/dpa> |
| Supplemental Terms for Azure Previews | Applies to preview features in AI Foundry | <https://azure.microsoft.com/support/legal/preview-supplemental-terms> |
| Microsoft Privacy Statement | Corporate privacy notice | <https://privacy.microsoft.com/privacystatement> |

## 4. Data Management

### 4.1 Server Location and Data Residency
- Hubs, projects and agent endpoints are **regional Azure resources**. Runtime data stays in the same Azure region you select (for example *UK South*, *UK West*).[^5]  
- Azure's Europe geography meets UK data-residency requirements and is assessed against the NCSC 14 Cloud Security Principles.[^6]

### 4.2 Data in Transit
- All traffic uses **TLS 1.2 or higher** by default; you can block weaker cipher suites through policy.[^7]  
- Private Link keeps traffic on the Microsoft backbone, removing exposure to the public internet.[^2]

### 4.3 Data at Rest
- Service-side encryption with **AES-256** is always on.[^8]  
- CMK (customer-managed keys) is supported for hubs, projects, agent threads and file storage.[^2][^9]

### 4.4 Data Retention
| Data type | Default retention | Administrator controls |
|-----------|------------------|------------------------|
| Agent Service threads and files | Persistent until caller deletes | Delete API |
| Application Insights logs | 90 days | 30–730 days configurable[^10] |
| Resource logs (Activity or Diagnostic) | 90 days | Azure Monitor retention policies |
| Model inputs and outputs | Not used for training; stored only in customer subscription unless logged through above features[^1] |

## 5. Audit Logging
- **Resource logs** for hubs and projects capture create and delete operations and can be exported to SIEM (security information and event management) tooling.[^4]  
- **Azure Monitor** and **Log Analytics** provide metric and query-based alerting.[^11]  
- Built-in Azure Policy definitions enforce that diagnostic settings are enabled and check compute resources for compliance.[^4]

## 6. Access Controls
- **Azure RBAC** roles such as *Hub Admin*, *Project Contributor* and custom roles govern least-privilege access.[^3]  
- **Managed identities** (system or user-assigned) avoid embedded secrets when Foundry interacts with other Azure services.[^2]  
- You can **disable** public network access at hub level; enforcement is possible through Deny policy.[^4]  

## 7. Compliance and Regulatory Requirements
Azure AI Foundry inherits Microsoft Azure's broad certification portfolio, including:

| Standard or Scheme | Status | Notes |
|-------------------|--------|-------|
| ISO/IEC 27001:2022 | Certified | Certificate available through Microsoft Service Trust Portal[^12] |
| SOC 2 Type 2 | Attested | Security, availability, processing integrity, confidentiality[^13] |
| GDPR | Compliant | Contractual commitments in DPA |
| HIPAA and HITRUST | Eligible workloads | BAA available on request[^14] |
| UK G-Cloud (NCSC 14 CSP) | Assessed | White-paper mapping Azure controls to 14 principles[^6] |

> **Note:** Responsibility for end-to-end compliance is shared. You must configure policies, retention and key-management to match your risk profile.

## 8. References
[^1]: *Data, privacy and security for use of models through the model catalogue*, Microsoft Learn, 19 May 2025.  
[^2]: *Policies for Azure AI Foundry hubs and projects*, Microsoft Learn, 11 Jun 2025.  
[^3]: *Role-based access control in Azure AI Foundry portal*, Microsoft Learn, 4 Jun 2025.  
[^4]: ibid., built-in policy definitions for logging and network controls.  
[^5]: *Azure AI Foundry Agent Service FAQ*, Microsoft Learn, 2025.  
[^6]: *UK G-Cloud – Azure Compliance*, Microsoft Learn.  
[^7]: *Enforce a minimum required version of TLS for Storage*, Microsoft Learn, 22 Mar 2024.  
[^8]: *Azure Storage encryption for data at rest*, Microsoft Learn, 13 Feb 2023.  
[^9]: *Customer-managed keys*, Microsoft Learn (linked from policy doc).  
[^10]: *Customer-enabled disaster recovery*, Microsoft Learn, Apr 2025.  
[^11]: *Azure AI Foundry architecture*, Microsoft Learn, 28 Apr 2025.  
[^12]: *ISO/IEC 27001 – Azure Compliance*, Microsoft Learn.  
[^13]: *System and Organisation Controls (SOC) 2 Type 2*, Microsoft Learn.  
[^14]: *HIPAA – Azure Compliance*, Microsoft Learn.
