# Azure AI Foundry - Summary

**Approval status:** Approved - you can use this tool within Defra when you follow the tool guidance advice.

This summary covers the key points from the [detailed guide](azure-ai-foundry-detailed.md). Use it to understand how Azure AI Foundry works in government environments.

## Tool Overview
Azure AI Foundry is a managed Azure service for designing, building and running generative AI workloads. It combines a model catalogue, multi-agent orchestration, managed compute and governance in one portal, SDK and set of REST APIs. Foundry resources live inside your Azure subscription, so your organisation keeps control of data and networking.

## Privacy Settings
* **Private networking** – isolate hubs and projects through Azure Private Link, blocking public internet access.  
* **Customer-managed keys (CMK)** – encrypt metadata and artefacts with keys you control in Azure Key Vault.  
* **Conditional Access & RBAC** – Microsoft Entra and Azure role-based access control restrict who can view or change resources.  
* **Diagnostic data opt-in** – administrators choose whether to send telemetry to Log Analytics or SIEM tooling.

## Terms of Use and Privacy Policy
* **Microsoft Product Terms** – main contract for Azure services, including preview disclaimers.  
* **Microsoft Products and Services Data Protection Addendum** – GDPR-aligned processing terms.  
* **Supplemental Terms for Azure Previews** – extra provisions for Foundry preview features.  
* **Microsoft Privacy Statement** – corporate privacy notice that applies to Azure.

## Data Management
### Multi-Regional Processing
Create Foundry hubs, projects and agent endpoints in a single Azure region (for example *UK South*). Runtime data stays in that region. Cross-region replication only happens if you enable disaster recovery.

### Data in Transit
* All service endpoints enforce TLS 1.2 or higher.  
* Private Link keeps traffic on the Microsoft backbone, avoiding the public internet.

### Data at Rest
* Microsoft encrypts all data with AES-256 as standard.  
* You can enable CMK for stronger control, allowing key rotation and revocation.  

## Auditing
* **Resource logs** record create, update and delete operations on hubs and projects.  
* Stream logs to Azure Monitor, Log Analytics or a third-party SIEM for retention and alerting.  
* Built-in Azure Policy rules enforce that logging and private networking stay switched on.

## Access Controls
* Fine-grained Azure RBAC roles (for example *Hub Owner*, *Project Contributor*) support least-privilege assignments.  
* Managed identities remove the need to embed secrets when Foundry components call other Azure services.  
* Disable public network access at hub level and enforce with Azure Policy.

## Compliance & Regulatory Considerations
Foundry inherits Azure's existing certifications:

| Standard or scheme | Status | Notes |
|--------------------|--------|-------|
| ISO/IEC 27001:2022 | Certified | Certificate available on Microsoft Service Trust Portal |
| SOC 2 Type 2 | Attested | Security, availability, processing integrity, confidentiality |
| GDPR | Compliant | Contractual commitments in Data Protection Addendum |
| UK G-Cloud (NCSC 14 CSP) | Assessed | White-paper mapping Azure controls to 14 principles |
| HIPAA & HITRUST | Eligible workloads | Business Associate Agreement available on request |
