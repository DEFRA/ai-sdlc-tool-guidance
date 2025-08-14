# CodeRabbit

## Tool Overview

CodeRabbit is an AI-powered code review platform that automates security analysis and code quality assessments for software development teams. Founded in 2023, the platform uses Large Language Models combined with Abstract Syntax Tree analysis to provide context-aware reviews across entire codebases.

The platform integrates with major version control systems including GitHub, GitLab, Azure DevOps and Bitbucket. It supports all major programming languages, with particular strengths in JavaScript, TypeScript, Python, Java and C#. Reviews typically complete within minutes of pull request submission.

For UK government use, significant considerations exist around data sovereignty, compliance requirements and contractual terms. The platform operates primarily from US-based infrastructure, which presents challenges for government adoption.

## Privacy Settings

CodeRabbit provides several privacy controls for organisations:

- **Zero-retention processing**: Code exists only in memory during analysis with immediate disposal after review completion
- **Opt-out mechanisms**: Comprehensive options for complete data storage opt-out
- **Model training isolation**: Proprietary code is never used to train AI models
- **Ephemeral environments**: Each review operates in isolated, temporary containers

The platform allows configuration of data retention periods:
- Vector embeddings for learning personalisation: 7-day cache retention (optional)
- Knowledge base issues from connected platforms: configurable retention
- Administrative data: retained as necessary for service provision
- GDPR-compliant deletion: 30 days upon request

## Terms of Use and Privacy Policy

The legal framework presents significant challenges for UK government adoption:

### Governing law and jurisdiction
- Terms governed by California law
- Mandatory arbitration requirements
- Liability caps set at the greater of amounts paid in last 6 months or $100

### Privacy policy considerations
- All data processing occurs on US servers
- Subject to US federal and state laws including potential FISA court orders
- Data Processing Agreement incorporates EU Standard Contractual Clauses
- 22 of 24 identified subprocessors are US-based (including OpenAI, Anthropic, Google Cloud Platform)

### UK government compatibility issues
- No UK-specific data residency options in standard offering
- Contractual terms incompatible with typical government requirements
- Inadequate liability provisions for public sector use

## Data Management

CodeRabbit implements a multi-layered approach to data handling:

### Processing architecture
- Google Cloud Platform infrastructure (US-based)
- Multi-availability zone replication for resilience
- Sandboxed execution through Google Cloud Run
- Jailing and cgroup restrictions for process isolation

### Data lifecycle
- Repository code processed ephemerally in memory
- No persistent storage of source code by default
- Optional persistent elements include vector embeddings and knowledge base data
- Complete data disposal immediately after review completion

### Backup and recovery
- Regular backup restoration testing
- Formal business continuity planning
- Recovery Time Objectives and Recovery Point Objectives not publicly disclosed

## Multi-Regional Processing

Current infrastructure limitations affect UK government suitability:

### Geographic distribution
- All processing occurs in US data centres
- No UK or EU data centre options available
- Multi-availability zone deployment within US regions only

### Self-hosted alternative
- Available on Enterprise plans (minimum 500 users)
- Enables complete data sovereignty within UK infrastructure
- Supports air-gapped operation for sensitive environments
- Transfers infrastructure management responsibility to the organisation

## Data in Transit

Security measures for data transmission include:

- Transport Layer Security (TLS) encryption for all connections
- Specific TLS versions and cipher suites not publicly documented
- OAuth 2.0 authentication protocols
- Webhook-based integration with version control platforms
- API endpoints with OpenAPI documentation for custom integrations

## Data at Rest

Data storage security incorporates:

### Encryption standards
- Encryption details not fully specified in public documentation
- Google Cloud Platform native encryption services utilised
- Ephemeral processing minimises data at rest requirements

### Storage locations
- All persistent storage in US-based Google Cloud Platform
- No option for UK-based storage in standard offering
- Self-hosted deployment allows complete control over storage location

## Auditing

The platform provides audit capabilities including:

- Access event logging
- Configuration change tracking
- Security incident recording
- Integration with Git platform audit trails
- SIEM integration capabilities not documented
- Log export formats not specified publicly

Annual third-party security assessments are conducted, though specific audit reports are not publicly available.

## Access Controls

Authentication and authorisation features include:

### Authentication methods
- Multi-factor authentication mandatory for all users
- OAuth 2.0 support
- Single Sign-On inheritance from connected Git platforms
- Azure Active Directory and Okta integration support

### Role-based access control
- Three-tier system: Admin, Member, Billing Admin
- Granular permissions management
- Least-privilege principles implementation
- Periodic access reviews
- Background checks for personnel with data access

### Integration security
- Operates within connected platform's permission framework
- Respects Git platform branch protection rules
- Cannot modify code or override platform security settings

## Compliance & Regulatory Considerations

### Current certifications
- **SOC 2 Type II**: Annual renewal with independent audits
- **ISO 27001:2022**: Information security management system compliance claimed
- **GDPR compliance**: Data Processing Agreement with Standard Contractual Clauses
- **HIPAA compliance**: Claimed but specific certification not provided

### Critical gaps for UK government
- **No Cyber Essentials or Cyber Essentials Plus certification**
- **No UK Government Security Classifications support** (OFFICIAL, SECRET)
- **No NHS Data Security and Protection Toolkit compliance**
- **No ICO registration evident**
- **No UK-specific contractual frameworks**

### Vulnerability management
- Vulnerability disclosure programme with monetary rewards ($100-$5,000)
- Risk-based patch management prioritising critical issues
- No traditional bug bounty platform presence

### Recommendations for UK government adoption
1. Self-hosted deployment essential for data sovereignty
2. Negotiate UK-specific contractual terms including:
   - UK governing law
   - Enhanced liability provisions
   - Government-appropriate service levels
3. Conduct comprehensive security assessment
4. Complete proof-of-concept with representative government codebases
5. Consider UK or EU-based alternatives for comparison
6. Evaluate vendor stability given 2023 founding date

## References

- CodeRabbit Terms of Service
- CodeRabbit Privacy Policy
- CodeRabbit Data Processing Agreement
- SOC 2 Type II certification (annual renewal)
- ISO 27001:2022 compliance statement
- GDPR Data Processing Agreement with Standard Contractual Clauses
- Data Protection Officer contact: dpo@coderabbit.ai

---

*Note: This evaluation is based on publicly available information and documentation. Organisations should conduct their own due diligence and security assessments before procurement decisions. The absence of UK-specific certifications and US-based infrastructure present significant barriers to immediate UK government adoption.*