# Azure AI Foundry

This summary provides essential information for UK government departments considering Azure AI Foundry for AI workloads. It covers security, privacy and compliance aspects relevant to public sector adoption.

## Tool Overview

Azure AI Foundry is Microsoft's unified platform for enterprise AI operations, launched in November 2024. It consolidates model deployment, fine-tuning and agent development into a single managed service.

The platform provides:
- access to over 100 AI models from Microsoft, OpenAI, Meta and other providers
- web-based portal (https://ai.azure.com/) and SDK for development
- project-based isolation for security boundaries
- retrieval-augmented generation (RAG) capabilities
- built-in content safety features

Government departments can use the service for document processing, business automation, conversational AI and data analysis whilst maintaining OFFICIAL data classification requirements.

## Privacy Settings

Azure AI Foundry implements comprehensive privacy controls suitable for government data:

- **Network isolation** - configure private endpoints and restrict internet exposure with "Allow Only Approved Outbound" traffic controls
- **Virtual network integration** - connect securely with existing government infrastructure without public internet exposure
- **Customer-managed encryption keys** - maintain control through Azure Key Vault with system-assigned or user-assigned managed identities
- **Project-level isolation** - separate file storage, thread storage and search indexes between departments and projects
- **Abuse monitoring opt-out** - disable data logging for content filtering on sensitive workloads (requires Microsoft approval)
- **Role-based access control** - integrate with Microsoft Entra ID, supporting conditional access and multi-factor authentication
- **IP network rules** - configure up to 200 specific address ranges for additional access restrictions

## Terms of Use and Privacy Policy

Government organisations engage through:
- **Microsoft Customer Agreement** for direct subscriptions
- **Enterprise Agreements** for volume licensing
- **Data Protection Addendum** establishing Microsoft as data processor with GDPR compliance

Key commitments:
- Customer data remains under government control
- No use for advertising or model improvement without explicit consent
- Prompt notification of government data requests unless legally prohibited
- Data processing within customer-designated geographies
- Over 90 compliance certifications accessible through Service Trust Portal

The Copilot Copyright Commitment provides indemnification against copyright claims when using recommended guardrails.

## Data Management

### Multi-Regional Processing

Azure operates two UK data centres certified to ISO 27001, SOC 2 and PCI DSS standards:
- **UK South** in London
- **UK West** in Cardiff

Geography-based storage controls ensure customer data remains within UK borders. Data at rest stays within the UK geography, with Microsoft only replicating between UK regions for redundancy. Single region residency is available when absolute data locality is required.

The service is approved for UK OFFICIAL data (approximately 90% of government information) through G-Cloud certification. SECRET and TOP SECRET classifications require additional secure networks beyond standard offerings.

### Data in Transit

All Azure AI services enforce robust encryption:
- **HTTPS with minimum TLS 1.2** using Perfect Forward Secrecy
- **2,048-bit RSA or 256-bit ECC keys** for key exchange
- **MACsec encryption** (IEEE 802.1AE) between Azure data centres
- **SHA-384 message authentication** and **AES-256 data encryption**

These measures exceed NCSC Principle 1 requirements for data in transit security, with automatic certificate management and key rotation.

### Data at Rest

Azure implements multiple layers of encryption:
- **FIPS 140-2 compliant 256-bit AES encryption** for all data
- **Transparent encryption** requiring no application modifications
- **Customer-managed keys** available via Hardware Security Modules in Azure Key Vault
- **Double encryption** option for additional protection layers

Azure Storage Service Encryption automatically protects blob storage, file shares and other storage services. Hardware-based security modules and cryptographic erasure capabilities align with NCSC principles for asset protection.

## Auditing

Azure Monitor provides comprehensive audit logging:

- **Three log categories**: control/management operations, data plane interactions, and security alerts from Microsoft Defender
- **90-day default retention** extending up to 12 years through Log Analytics
- **Multiple export formats**: CSV, JSON and others via PowerShell, Azure CLI and REST APIs
- **Real-time streaming** to SIEM systems through Azure Event Hubs
- **Immutability features**: system-generated logs that cannot be modified, WORM blob storage for archives

The platform meets NCSC audit requirements (Principle 13) with comprehensive logging for monitoring access and detecting security incidents. Native integration with Microsoft Sentinel and support for Splunk, QRadar and other government SIEM platforms.

## Access Controls

Azure AI Foundry uses Microsoft Entra ID for identity management with:

**Authentication methods:**
- Single sign-on across government Microsoft 365 estates
- Multi-factor authentication (mobile apps, SMS, voice calls, smart cards)
- Managed identities with automatic credential rotation
- Service principals with certificate and secret-based options

**Role-based access control:**
- Five dedicated AI service roles (User, Developer, Project Manager, Account Owner, Administrator)
- Integration with 65+ built-in Azure roles
- Privileged Identity Management for just-in-time access
- Approval workflows and time-bound assignments

**Zero-trust architecture:**
- Continuous verification
- Least-privilege access
- Device compliance checking
- Network micro-segmentation

Identity federation supports SAML 2.0 and OpenID Connect for integration with existing government identity providers.

## Compliance & Regulatory Considerations

Azure AI Foundry maintains extensive certifications for UK government use:

**International standards:**
- ISO/IEC 27001:2022 for information security management
- ISO/IEC 42001:2023 for AI management systems (achieved 2024)
- SOC 1, 2 and 3 reports confirming security and availability controls

**UK-specific compliance:**
- UK Cyber Essentials Plus with annual third-party validation
- G-Cloud Framework listing for UK OFFICIAL data
- NCSC 14 Cloud Security Principles compliance through annual attestation
- GDPR and UK Data Protection Act 2018 compliance

**Sector requirements:**
- NHS-specific compliance through UK OFFICIAL and UK NHS Azure Policy initiatives
- PCI DSS for payment processing
- FCA alignment for financial services

Azure Policy enables continuous compliance monitoring with built-in initiatives for UK government requirements. Over 90 compliance offerings are accessible through the Service Trust Portal.

## References

### Core documentation
- Azure AI Foundry overview: https://learn.microsoft.com/azure/ai-foundry/
- Service portal: https://ai.azure.com/
- Product information: https://azure.microsoft.com/products/ai-foundry

### Security and privacy
- Data privacy concepts: https://learn.microsoft.com/azure/ai-foundry/how-to/concept-data-privacy
- Network configuration: https://learn.microsoft.com/azure/ai-foundry/how-to/configure-private-link
- Encryption at rest: https://learn.microsoft.com/azure/ai-services/openai/encrypt-data-at-rest
- RBAC implementation: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-azure-ai-foundry

### Legal and compliance
- Microsoft Privacy Statement: https://privacy.microsoft.com/privacystatement
- Data Protection Addendum: https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA
- Service Trust Portal: https://servicetrust.microsoft.com/
- Azure legal information: https://azure.microsoft.com/support/legal/

### UK government guidance
- NCSC Cloud Security Principles: https://www.ncsc.gov.uk/collection/cloud/the-cloud-security-principles
- Government Security Classifications: https://www.gov.uk/government/publications/government-security-classifications
- G-Cloud guidance: https://www.gov.uk/guidance/g-cloud-suppliers-guide
- AI regulation approach: https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach