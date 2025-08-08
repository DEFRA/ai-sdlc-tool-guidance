# Azure AI Foundry - Summary

This summary covers the key points from the [detailed guide](azure-ai-foundry-detailed.md). Use it to understand how Azure AI Foundry works in government environments.

## What Azure AI Foundry does

Azure AI Foundry is Microsoft's unified cloud platform for designing, building, and running generative AI applications at enterprise scale. It provides access to foundation models, enables sophisticated multi-agent workflows, and delivers governance capabilities through Azure's secure infrastructure.

You can deploy Azure AI Foundry in different configurations:
- **Standard hub deployment:** Models and agents run in Azure public cloud regions
- **Private networking:** Connect without using the public internet (Azure Private Link)
- **Customer-managed keys:** Full control over encryption keys through Azure Key Vault
- **Local inference:** Deploy open-source models on local devices and edge infrastructure (Windows AI Foundry)

## Privacy controls

Azure AI Foundry protects your data by default, particularly following Microsoft's ISO/IEC 42001:2023 certification achievement in July 2025:
- **No model training:** Your data does not train or improve AI models (this is the default setting)
- **Private networking:** Keep traffic off the public internet using Azure Private Link
- **Customer-managed keys:** Full control over encryption keys through Azure Key Vault integration
- **Agent thread privacy:** Configurable retention policies for AI agent conversation threads with customer-controlled deletion

## Terms and data ownership

Key legal points:
- **You own your content:** Customer content (inputs and outputs) belongs to you, not Microsoft
- **Unified model terms:** Microsoft manages model provider relationships, reducing licensing complexity
- **Data protection compliance:** Microsoft terms cover GDPR and UK data protection laws with strengthened commitments following ISO/IEC 42001:2023 certification
- **Content restrictions:** Terms ban generating illegal or harmful content, with built-in content safety filters

## Where your data goes

### Location and residency

- **UK regions available:** Process data in Azure UK South or UK West regions to meet UK data residency requirements
- **Regional boundaries:** Data stays in the region you choose, with clear separation between regions
- **Comprehensive isolation:** All components including fine-tuning, agent threads, and knowledge bases remain in your selected region
- **Legal jurisdiction:** UK region data follows UK law (though Microsoft as a US company also follows US requirements)

### Data protection in transit

All communication uses TLS 1.2 or higher encryption. Extra security options include:
- **Azure Private Link:** Traffic never goes over the public internet
- **Entra authentication:** Prevents tampering with API requests through Azure Active Directory
- **Certificate pinning:** Additional encryption validation for high-security environments

### Data protection at rest

- **Standard use:** Azure AI Foundry does not store your requests or responses permanently
- **Feature storage:** Fine-tuning data, agent threads, and knowledge bases use AES-256 encryption
- **Key management:** Use Azure Key Vault to control your own encryption keys with full sovereignty
- **Data deletion:** Delete custom models, agent conversations, and datasets when you no longer need them

## Audit logs

Azure AI Foundry connects to Azure's comprehensive logging systems:
- **Azure Activity Log:** Records all management operations with user identity, time, source IP, and operation details
- **Azure Monitor:** Tracks model operations, agent interactions, and can optionally log content
- **Agent Thread Logging:** Monitors conversation flows and agent reasoning processes when enabled
- **Content Safety Logging:** Tracks content filtering actions and policy violations
- **Responsible AI Evaluation:** Stores model bias assessments and safety evaluation results

## Access controls

Azure AI Foundry uses multiple security layers:
- **Azure RBAC:** Role-based access control defining which actions users can perform on which resources
- **Azure Policy:** Governance controls attached directly to hubs, projects, or deployments
- **Conditional Access:** Context-aware access control based on user risk, device compliance, and location
- **Managed Identities:** Eliminates embedded secrets for service-to-service authentication
- **Network controls:** Use Private Link and Network Security Groups to control network access

## Compliance and regulation

Azure AI Foundry benefits from Microsoft's compliance programmes, with significant recent achievements:
- **Responsible AI certification:** ISO/IEC 42001:2023 certification achieved July 2025 for Azure AI Foundry Models
- **Security certifications:** ISO/IEC 27001:2022, SOC 2 Type 2 covering Azure infrastructure
- **UK government:** UK G-Cloud listing, alignment with NCSC 14 Cloud Security Principles
- **Data protection:** GDPR and UK Data Protection Act 2018 compliance through contractual commitments
- **Industry-specific:** HIPAA eligibility, financial services compliance configurations available
- **AI governance:** Built-in content safety, bias evaluation, explainability features for emerging AI regulations
