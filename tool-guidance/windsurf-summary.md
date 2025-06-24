# Windsurf - Summary

This summary covers the key points from the [detailed guide](windsurf-detailed.md). Use it to understand how Windsurf can work in government environments.

## What Windsurf does

Windsurf IDE is an AI-powered integrated development environment built by Exafunction, Inc.

### Key capabilities

Windsurf provides several AI-enhanced coding features:

- **AI autocomplete** - unlimited code suggestions as you type
- **In-editor AI chat** - direct conversation with AI for code explanations and generation
- **Cascade agentic AI** - an AI agent that can perform multi-step coding tasks autonomously with your oversight
- **Natural language commands** - ability to execute coding tasks by describing intent in plain English
- **Integrated web preview** - live preview of web applications with AI-driven modifications
- **Model flexibility** - supports multiple AI providers including OpenAI, Anthropic, and Windsurf's own models

## Privacy controls

Windsurf offers strong privacy controls designed for enterprise and government use.

### Zero-data retention mode

- **Default for enterprise users** - no code data stored on Windsurf's servers
- **Optional for individual users** - can be enabled in profile settings
- Code sent to AI is processed in memory only and never written to disk or database
- Guarantees that code will not be used to train AI models

### Feature controls

Enterprise administrators can:

- Disable specific external AI model providers
- Control which models team members can access
- Enable or disable web search integration (off by default for enterprise)
- Manage data retention preferences for additional features

### Account management

- Self-serve account deletion available
- Personal data removed upon account deletion
- Acceptable Use Policy monitoring (with limited exceptions for abuse investigation)

## Terms of use and privacy policy

### Service terms

- Separate terms for individual/pro users and enterprise/team customers
- You retain ownership of code you write or AI generates
- Minimum age requirement of 13 years
- Standard liability limitations and arbitration clauses
- Last updated June 2025

### Privacy commitments

- Clear distinction between data controller and processor roles
- Support for Data Processing Agreements for enterprise customers
- Commitment to data protection best practices
- Contact mechanisms for privacy inquiries and data subject rights

### International considerations

- Data may be transferred to and processed in the United States
- EU/UK transfers handled through appropriate legal mechanisms
- Frankfurt-based EU cluster available for European data residency requirements

## Where your data goes

### Multi-regional processing

Windsurf offers several deployment options to meet different data residency requirements:

#### Standard cloud deployment
- **Location**: United States (Google Cloud Platform)
- **Suitable for**: General enterprise use where US data processing is acceptable

#### EU cluster
- **Location**: Frankfurt, Germany
- **Suitable for**: European organisations requiring EU data residency
- **Benefits**: Keeps code data within European jurisdiction

#### FedRAMP High environment
- **Location**: AWS GovCloud (US)
- **Suitable for**: US federal agencies handling sensitive unclassified data
- **Compliance**: DoD Impact Level 5 and ITAR authorised

#### Hybrid deployment
- **Configuration**: Customer-managed components on-premises, AI compute in Windsurf cloud
- **Benefits**: Data storage under your control, secure outbound-only connections
- **Connection**: Encrypted Cloudflare Tunnel (no inbound firewall changes required)

#### Self-hosted deployment
- **Configuration**: Complete Windsurf stack within your infrastructure
- **Benefits**: No data ever leaves your network, maximum sovereignty
- **Requirements**: You manage AI model endpoints and infrastructure

### Data protection in transit

All data transmission is protected through industry-standard encryption:

- **TLS encryption** for all client-server communications
- **HTTPS/TLS** for third-party model API connections
- **End-to-end encrypted tunnels** for hybrid deployments
- **Minimal context transmission** - only necessary code snippets sent, not entire files

### Data protection at rest

#### Windsurf cloud storage
- **Enterprise default**: Zero retention of code data
- **Individual users**: Optional code logging for service improvement (limited retention)
- **Encryption**: All stored data encrypted at rest using cloud provider security standards
- **Metadata only**: Usage analytics stored without actual code content

#### Customer-controlled storage
- **Hybrid mode**: Code indices and logs stored on your infrastructure
- **Self-hosted**: All data remains within your environment
- **Encryption**: Standard disk encryption applied per your policies

#### Retention policies
- **Code data**: Not retained with zero-retention mode enabled
- **Account data**: Retained while account active, deleted upon account closure
- **Prompt caching**: Temporary cache (minutes to hours) for performance optimisation
- **Abuse logs**: Limited retention for policy violation investigation only

## Audit logs

### Audit logging capabilities

Available in enterprise hybrid and self-hosted deployments:

- **Comprehensive tracking**: Every accepted AI suggestion and chat conversation logged
- **Local storage**: All audit data stored within your environment, not on Windsurf servers
- **Detailed records**: Timestamps, content, file locations, and user identification
- **Traceability**: Full visibility into AI contributions to codebase

### Attribution logging

- **Code matching**: Records when generated code closely matches known open-source code
- **Compliance support**: Helps identify potential intellectual property concerns
- **Local storage**: Attribution logs kept within customer-controlled infrastructure

### Limitations

- Audit logging currently limited to non-cloud (hybrid/self-hosted) deployments
- Pure SaaS customers may not have access to detailed logging features
- Trade-off between convenience and audit capability

## Access controls

### User authentication

- **Account-based access** with email/password or single sign-on
- **SSO integration** via SAML (Microsoft Entra ID, Okta, Google Workspace)
- **Multi-factor authentication** support through SSO providers
- **SCIM provisioning** for automated user lifecycle management

### Administrative controls

#### Team management
- **Hierarchical roles**: Team admins, group admins, standard users
- **User groups**: Departmental or project-based segregation
- **Delegated administration**: Group-level oversight without global access

#### Feature management
- **AI model selection**: Control which AI providers are available
- **Feature toggles**: Enable/disable specific capabilities like web search
- **Safety controls**: No automatic command execution for enterprise users
- **Change approval**: All AI modifications require explicit user acceptance

### Operational safeguards

- **No auto-execution**: Terminal commands require manual approval
- **Draft mode changes**: AI edits not automatically saved or committed
- **Version control integration**: Standard Git workflows maintained
- **Session isolation**: User data and sessions completely separated

## Compliance and regulation

### Security certifications

#### SOC 2 Type II
- Third-party audited security, availability, and confidentiality controls
- Reports available under NDA through Windsurf Trust Centre
- Ongoing operational effectiveness demonstration

#### FedRAMP High authorisation
- Highest baseline US government cloud security accreditation
- Suitable for sensitive unclassified data
- Continuous monitoring and vulnerability management requirements

#### Industry-specific compliance
- **DoD Impact Level 5**: Department of Defense controlled unclassified information
- **ITAR compliance**: Defence-related technical data handling
- **HIPAA compliance**: Protected health information safeguards with Business Associate Agreements

### Data protection alignment

#### UK/EU considerations
- **GDPR compliance approach**: Data Processing Agreements available
- **UK GDPR alignment**: EU hosting option supports adequacy framework
- **Data subject rights**: Account deletion and privacy inquiry mechanisms
- **Lawful basis**: Clear processor/controller relationship definition

#### Risk mitigation
- **Intellectual property protection**: Technical measures to avoid licensed code generation
- **Indemnity provisions**: Enterprise protection against third-party IP claims
- **Vulnerability management**: Regular penetration testing and security researcher engagement
- **Continuous improvement**: Active security monitoring and patch management

### Regulatory gaps

- No specific ISO 27001 certification mentioned
- UK-specific data centre not currently available (EU Frankfurt option exists)
- Some features require hybrid/self-hosted deployment for full compliance benefit
