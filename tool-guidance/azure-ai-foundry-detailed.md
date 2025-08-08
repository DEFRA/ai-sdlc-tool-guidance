# Azure AI Foundry evaluation for UK government adoption

## Executive summary

**Azure AI Foundry meets UK government requirements for OFFICIAL data classification and demonstrates compliance with
NCSC's 14 Cloud Security Principles**. Microsoft's unified AI platform, launched in November 2024, provides
enterprise-grade security controls, UK-based data centres, and holds necessary certifications including UK Cyber
Essentials Plus and G-Cloud listing. The service implements FIPS 140-2 compliant encryption, comprehensive audit
logging, and role-based access controls suitable for government deployment.

The platform offers robust data sovereignty with UK data centres in London and Cardiff, customer-managed encryption
keys, and configurable retention policies. Key compliance achievements include ISO 27001:2022, SOC 2 Type 2, and the
recent ISO/IEC 42001:2023 certification for AI management systems. Whilst approved for UK OFFICIAL data, departments
handling SECRET or TOP SECRET classifications would require additional security arrangements beyond the standard
offering.

This evaluation finds Azure AI Foundry technically suitable for UK government adoption for OFFICIAL data workloads,
contingent upon appropriate configuration of privacy settings, implementation of recommended security controls, and
adherence to government AI regulatory principles.

## 1. Tool overview

Azure AI Foundry represents Microsoft's comprehensive platform-as-a-service solution for enterprise AI operations,
consolidating model deployment, fine-tuning, and agent development into a unified environment. The platform replaced
Azure AI Studio in November 2024, providing government organisations with access to over 100 AI models from Microsoft,
OpenAI, Meta, and other providers through a single API interface.

The service comprises two primary components: the **Azure AI Foundry Portal** (https://ai.azure.com/) offering a
web-based graphical interface for project management, and the **Azure AI Foundry SDK** providing code-first development
capabilities. Government departments can leverage these tools for document processing, business process automation,
conversational AI, and intelligent data analysis whilst maintaining security isolation through project-based boundaries.

**Core capabilities** include retrieval-augmented generation (RAG) for integrating proprietary data sources, fine-tuning
for department-specific requirements, and built-in content safety features essential for public-sector deployments. The
platform's **agent service** enables creation of intelligent assistants that can navigate complex government workflows
whilst maintaining audit trails and access controls required for public accountability.

Official documentation: https://learn.microsoft.com/azure/ai-foundry/  
Service portal: https://azure.microsoft.com/products/ai-foundry

## 2. Privacy settings

Azure AI Foundry implements multiple privacy controls essential for government data protection. **Network isolation**
capabilities allow departments to configure private endpoints and restrict internet exposure, with options for "Allow
Only Approved Outbound" traffic ensuring data remains within controlled boundaries. The platform supports **virtual
network integration** with existing government infrastructure, enabling secure communication without public internet
exposure.

**Customer-managed encryption keys** stored in Azure Key Vault provide departments with control over data encryption,
supporting both system-assigned and user-assigned managed identities. The service implements **project-level isolation
**, ensuring that each government project maintains separate file storage, thread storage, and search indexes with no
cross-contamination between departments or projects.

**Abuse monitoring can be disabled** for sensitive government workloads through Microsoft's approval process, preventing
any data logging for content filtering purposes. **Role-based access control** integrates with Microsoft Entra ID,
supporting conditional access policies and multi-factor authentication requirements standard across government IT
estates. Departments can configure **IP network rules** supporting up to 200 specific address ranges for additional
access restrictions.

Configuration guides:  
Network configuration: https://learn.microsoft.com/azure/ai-foundry/how-to/configure-private-link  
Security settings: https://learn.microsoft.com/azure/ai-foundry/how-to/secure-data-playground  
RBAC configuration: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-azure-ai-foundry

## 3. Terms of use and privacy policy

Government organisations engage with Azure AI Foundry through either the **Microsoft Customer Agreement** for direct
subscriptions or **Enterprise Agreements** for volume licensing arrangements. The **Data Protection Addendum
** (https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA) governs
customer data processing, establishing Microsoft as data processor with explicit GDPR compliance frameworks applicable
to UK organisations.

Microsoft's **Privacy Statement** (https://privacy.microsoft.com/privacystatement) confirms that customer data remains
under government control, with no use for advertising or model improvement without explicit consent. The **Copilot
Copyright Commitment** provides indemnification against copyright claims when using recommended guardrails, addressing
intellectual property concerns for government content generation.

**Critical for government use**: Microsoft commits to prompt notification of government data requests unless legally
prohibited, maintains data processing within customer-designated geographies, and provides over 90 compliance
certifications accessible through the Service Trust Portal (https://servicetrust.microsoft.com/). Preview features
operate under supplemental terms (https://azure.microsoft.com/support/legal/preview-supplemental-terms) and should be
evaluated carefully for production government workloads.

Legal framework: https://azure.microsoft.com/support/legal/  
AI-specific privacy: https://learn.microsoft.com/azure/ai-foundry/how-to/concept-data-privacy

## 4. Data management

### 4.1 Server location and data residency

Azure operates **two UK data centres**: UK South in London and UK West in Cardiff, both certified to ISO 27001, SOC 2,
and PCI DSS standards. These facilities enable government departments to maintain data sovereignty within UK borders,
meeting requirements for OFFICIAL data classification comprising approximately 90% of government information.

The platform provides **geography-based storage controls** ensuring customer data remains within specified regions. For
UK deployments, data at rest stays within the UK geography, with Microsoft only replicating between UK regions for
redundancy. **Single region residency** requires explicit configuration but ensures absolute data locality when
regulatory requirements demand it.

**UK government restrictions** permit Azure for OFFICIAL data through G-Cloud certification, with annual attestation of
NCSC compliance. SECRET and TOP SECRET classifications require additional secure networks beyond standard Azure
offerings. Brexit considerations remain addressed through UK's EU data adequacy status, extended to December 2025.

UK infrastructure details: https://azure.microsoft.com/global-infrastructure/data-residency  
G-Cloud compliance: https://learn.microsoft.com/azure/compliance/offerings/offering-uk-g-cloud

### 4.2 Data in transit

All Azure AI services enforce **HTTPS with minimum TLS 1.2** for data transmission, implementing Perfect Forward Secrecy
with 2,048-bit RSA or 256-bit ECC keys. **MACsec encryption** (IEEE 802.1AE) automatically protects all traffic between
Azure data centres, preventing physical interception without customer configuration requirements.

The platform implements **SHA-384 message authentication** and **AES-256 data encryption** for transit protection,
exceeding NCSC Principle 1 requirements for data in transit security. Certificate management occurs transparently with
automatic key rotation and no customer intervention required for standard deployments.

**UK government requirements** mandate protection against tampering and eavesdropping, which Azure meets through its
multi-layered encryption approach. The annual G-Cloud attestation confirms ongoing compliance with these transit
security principles.

Encryption overview: https://learn.microsoft.com/azure/security/fundamentals/encryption-overview

### 4.3 Data at rest

Azure implements **FIPS 140-2 compliant 256-bit AES encryption** for all data at rest, with transparent
encryption/decryption requiring no application modifications. Government departments can choose between
Microsoft-managed keys for baseline protection or **customer-managed keys** stored in Hardware Security Modules via
Azure Key Vault for enhanced control.

**Azure Storage Service Encryption** automatically protects blob storage, file shares, and other storage services used
by AI Foundry. The platform supports **double encryption** for departments requiring additional protection layers,
implementing independent encryption at both infrastructure and service layers.

**UK government requirements** for asset protection and resilience are met through hardware-based security modules,
cryptographic erasure capabilities, and comprehensive key management aligned with NCSC principles. RSA and RSA-HSM keys
of 2048-bit size provide enterprise-grade protection for encryption operations.

Encryption configuration: https://learn.microsoft.com/azure/ai-services/openai/encrypt-data-at-rest  
Key management: https://learn.microsoft.com/azure/ai-foundry/concepts/encryption-keys-portal

### 4.4 Data retention

Azure AI Foundry implements **no default retention** for prompts and completions in the base service, processing them in
real-time without storage. Deleted resources enter a **48-hour recovery window** before permanent purging, providing
protection against accidental deletion whilst ensuring eventual data removal.

**Customer-controlled retention policies** enable departments to configure storage lifecycle management from days to
years, supporting regulatory requirements through automated tier transitions and deletion rules. **Log Analytics
retention** defaults to 30 days but extends up to 12 years for compliance needs, with archive tiers available for
long-term storage at reduced cost.

**Fine-tuning data** remains under customer control until explicit deletion, never used for model improvement without
consent. The platform implements **cryptographic erasure** through customer-managed key revocation, immediately
rendering encrypted data unrecoverable for immediate compliance with data subject requests.

Retention configuration: https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-policy-configure  
Recovery procedures: https://learn.microsoft.com/azure/ai-services/recover-purge-resources

## 5. Audit logging

Azure Monitor provides **comprehensive audit logging** across all AI services, capturing control plane operations
through Activity Logs with 90-day default retention. **Three log categories** track government usage: control/management
logs for resource operations, data plane logs for service interactions, and processed events from Microsoft Defender for
Cloud security alerts.

**Extended retention** up to 12 years through Log Analytics workspace enables long-term compliance with government audit
requirements. Logs export in CSV, JSON, and other formats via PowerShell, Azure CLI, and REST APIs, supporting
integration with existing government monitoring infrastructure. **Real-time streaming** to SIEM systems occurs through
Azure Event Hubs with 5-minute batching intervals.

**Immutability features** include system-generated logs that cannot be modified, WORM (Write Once, Read Many) blob
storage for archives, and comprehensive audit trails for log access. Microsoft Sentinel provides native threat detection
whilst supporting integration with Splunk, QRadar, and other SIEM platforms commonly used in government.

The platform meets **NCSC audit requirements** through comprehensive logging aligned with Principle 13, providing
records necessary to monitor access to services and detect potential security incidents.

Azure Monitor documentation: https://learn.microsoft.com/azure/security/fundamentals/log-audit  
SIEM integration: https://learn.microsoft.com/azure/azure-monitor/logs/stream-logs-to-event-hubs

## 6. Access controls

Azure AI Foundry leverages **Microsoft Entra ID** for enterprise identity management, implementing single sign-on across
government Microsoft 365 estates. **Multi-factor authentication** enforces additional verification for privileged
operations, supporting mobile apps, SMS, voice calls, and smart card authentication methods standard in government.

**Five dedicated RBAC roles** control AI service access: Azure AI User (reader access), Azure AI Developer (development
permissions), Azure AI Project Manager (project management), Azure AI Account Owner (full access), and Azure AI
Administrator (managed identity permissions). These integrate with 65+ built-in Azure roles, enabling **granular
permission management** aligned with government separation of duties requirements.

**Privileged Identity Management** provides just-in-time access with approval workflows, time-bound assignments, and
mandatory business justification for sensitive operations. **Zero-trust architecture** implements continuous
verification, least-privilege access, device compliance checking, and network micro-segmentation essential for
government security postures.

**Managed identities** eliminate password management through automatic credential rotation, whilst **service principals
** enable application authentication with certificate and secret-based options. Identity federation supports SAML 2.0
and OpenID Connect for integration with existing government identity providers.

RBAC guide: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-azure-ai-foundry  
Identity documentation: https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview

## 7. Compliance and regulatory requirements

Azure AI Foundry maintains **extensive compliance certifications** essential for UK government adoption. **ISO/IEC
27001:2022** certification validates information security management, whilst **SOC 1, 2, and 3 reports** confirm
security, availability, and processing integrity controls. The platform achieved **ISO/IEC 42001:2023** certification in
2024, becoming one of the first AI services certified for AI management systems.

**UK-specific certifications** include **UK Cyber Essentials Plus** covering production systems with annual third-party
validation, and **G-Cloud Framework listing** confirming suitability for UK OFFICIAL data. The service demonstrates *
*NCSC 14 Cloud Security Principles** compliance through annual attestation, meeting foundational government cloud
requirements.

**GDPR and UK Data Protection Act 2018** compliance features comprehensive data subject rights support, privacy by
design implementation, and 72-hour breach notification capabilities. **NHS-specific compliance** addresses healthcare
requirements through UK OFFICIAL and UK NHS Azure Policy initiatives, supporting Data Security and Protection Toolkit
requirements.

The platform provides **90+ compliance offerings** including PCI DSS for payment processing, FCA alignment for financial
services, and sector-specific certifications accessible through the Service Trust Portal. **Azure Policy** enables
continuous compliance monitoring with built-in initiatives for UK government requirements.

ISO 27001 details: https://learn.microsoft.com/azure/compliance/offerings/offering-iso-27001  
UK Cyber Essentials: https://learn.microsoft.com/azure/compliance/offerings/offering-uk-cyber-essentials-plus  
Service Trust Portal: https://servicetrust.microsoft.com/

## 8. References

### Microsoft Azure AI Foundry documentation

- Azure AI Foundry overview: https://learn.microsoft.com/azure/ai-foundry/
- Service portal: https://ai.azure.com/
- Product information: https://azure.microsoft.com/products/ai-foundry

### Security and privacy resources

- Data privacy concepts: https://learn.microsoft.com/azure/ai-foundry/how-to/concept-data-privacy
- Network configuration: https://learn.microsoft.com/azure/ai-foundry/how-to/configure-private-link
- Encryption at rest: https://learn.microsoft.com/azure/ai-services/openai/encrypt-data-at-rest
- RBAC implementation: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-azure-ai-foundry

### Legal and compliance documentation

- Microsoft Privacy Statement: https://privacy.microsoft.com/privacystatement
- Data Protection
  Addendum: https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA
- Azure legal information: https://azure.microsoft.com/support/legal/
- Service Trust Portal: https://servicetrust.microsoft.com/

### UK government resources

- NCSC Cloud Security Principles: https://www.ncsc.gov.uk/collection/cloud/the-cloud-security-principles
- Government Security Classifications: https://www.gov.uk/government/publications/government-security-classifications
- G-Cloud guidance: https://www.gov.uk/guidance/g-cloud-suppliers-guide
- AI regulation approach: https://www.gov.uk/government/publications/ai-regulation-a-pro-innovation-approach

### Azure compliance certifications

- ISO 27001: https://learn.microsoft.com/azure/compliance/offerings/offering-iso-27001
- UK Cyber Essentials Plus: https://learn.microsoft.com/azure/compliance/offerings/offering-uk-cyber-essentials-plus
- UK G-Cloud: https://learn.microsoft.com/azure/compliance/offerings/offering-uk-g-cloud
- Trust Center: https://www.microsoft.com/trust-center

### Data management and infrastructure

- Azure global infrastructure: https://azure.microsoft.com/global-infrastructure/data-residency
- Encryption overview: https://learn.microsoft.com/azure/security/fundamentals/encryption-overview
- Storage lifecycle management: https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-policy-configure
- Audit logging: https://learn.microsoft.com/azure/security/fundamentals/log-audit