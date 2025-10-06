# JetBrains Junie

## Tool Overview

JetBrains Junie is an AI coding agent that autonomously plans and executes complex programming tasks within JetBrains integrated development environments (IDEs). Unlike traditional AI coding assistants that provide suggestions, Junie operates autonomously - navigating project files, running code, executing terminal commands, and modifying file systems based on natural language instructions.

### Key characteristics

- **Mandatory cloud processing**: Requires continuous internet connectivity with no offline mode available
- **Third-party AI providers**: Uses OpenAI (GPT-5) or Anthropic (Claude) models hosted in the United States
- **IDE integration**: Available as a plugin for IntelliJ IDEA, PyCharm, WebStorm, and other JetBrains IDEs
- **Licensing tiers**: AI Free, Pro, Ultimate, and Enterprise (with on-premises options for Enterprise only)

### Critical limitation for government use

Standard licences require all code and prompts to be transmitted to US-based AI providers, raising significant data sovereignty concerns for UK government use.

## Privacy Settings

### Available controls

Junie provides several privacy controls at the project level:

- **.aiignore file**: Specifies files and folders requiring explicit approval before access
- **Approved directory**: Designates where Junie can modify files without confirmation
- **Action allowlist**: Controls which terminal commands can execute without approval
- **Brave mode**: Allows terminal commands without explicit approval (less secure)

### Data collection options

- **Zero data retention (default)**: JetBrains doesn't store data, but third-party providers retain for 7-30 days
- **Detailed data collection**: Optional opt-in for sharing prompts and code snippets with JetBrains (30-day retention)

### Critical gaps

- No option to operate offline or with local models
- Cannot disable data sharing with third-party providers whilst using the service
- No UK-only or EU-only data processing options for standard licences
- Cannot configure third-party retention periods without enterprise arrangements

## Terms of Use and Privacy Policy

### Key contractual concerns

**Liability limitations**:
- Service provided "as is" with no express warranties
- Maximum liability capped at $100 USD or 6 months' fees
- No guaranteed service level agreements

**Data processing**:
- Governed by Czech Republic law (JetBrains s.r.o.)
- Strong GDPR compliance framework with designated Data Protection Officer
- Users prohibited from inputting personal data
- Customer solely responsible for data sensitivity assessment

### Privacy policy highlights

JetBrains demonstrates comprehensive GDPR compliance as an EU entity, including:
- All data subject rights implemented
- Standard Contractual Clauses for international transfers
- Clear legal bases for processing
- Data Processing Agreement available

However, post-Brexit UK GDPR compliance isn't explicitly confirmed, requiring additional verification for government procurement.

## Data Management

### Multi-Regional Processing

**Infrastructure**: Amazon Web Services and Google Cloud Platform across EU, US, and Asia regions

**Third-party AI provider locations**:
- OpenAI: Primarily US-based processing
- Anthropic: US-based operations
- Google Vertex AI: Multi-region (EU configuration requires enterprise setup)

**UK data sovereignty assessment**:
- Standard licences: **Fail** - Data leaves UK/EU jurisdiction to US providers
- Enterprise licence: **Conditional pass** - Only with on-premises deployment or regional configuration

The US CLOUD Act poses additional sovereignty risks, potentially compelling US providers to disclose data regardless of storage location.

### Data in Transit

- **Encryption standard**: Transport Layer Security (TLS)
- **Assessment**: Industry-standard encryption
- **Gap**: Specific TLS version (1.2 vs 1.3) not documented

### Data at Rest

- **Encryption method**: AES-256 for all storage
- **Key management**: Regular rotation with restricted access
- **Assessment**: Industry-standard encryption

### Data Retention

**JetBrains retention**:
- Default: Zero data retention on JetBrains servers
- Opt-in: Maximum 30 days for detailed data collection

**Third-party provider retention**:
- OpenAI: 30 days for abuse monitoring
- Anthropic: 7 days (reducing from 30 days in September 2025)
- Google Vertex AI: 24-hour caching by default

Zero data retention from third parties requires separate enterprise negotiations not included in standard licences.

## Auditing

### Critical finding

**No comprehensive audit logging capabilities documented**. The tool lacks:
- Persistent activity logs
- Administrator-accessible audit trails
- User action tracking for compliance
- Security event monitoring
- File modification records
- Failed attempt logging

### Available monitoring

Limited to:
- AI Credits consumption tracking
- Real-time visibility during active sessions
- Changed files list after task completion

This represents a critical gap for environments requiring audit trails for security compliance or regulatory requirements.

## Access Controls

### Authentication and authorisation

- Requires JetBrains Account for activation
- No multi-factor authentication explicitly documented
- Licence tiers primarily differ in quota rather than permissions

### Organisation controls (Enterprise only)

Administrators can:
- Enable/disable JetBrains AI for all users
- Set usage limits and AI Credits caps
- Configure available AI providers
- Control data collection settings

### Project-level controls

- Approved directories for modification
- .aiignore files for access restrictions
- Action allowlists for terminal commands

### Critical gaps

- No granular role-based access control
- No git-specific permission controls
- No integration with government identity providers documented
- No network-level access restrictions

## Compliance & Regulatory Considerations

### Confirmed certifications

**SOC 2 Type II**: Achieved February 2024 for security, availability, processing integrity, confidentiality, and privacy. However, Junie not explicitly included in audit scope.

**GDPR compliance**: Comprehensive EU GDPR compliance as Czech Republic entity with Data Protection Officer and full framework implementation.

### UK-specific standards gaps

- **Cyber Essentials**: Not certified
- **Cyber Essentials Plus**: Not certified
- **ISO 27001**: Not independently certified (relies on infrastructure providers)
- **NCSC Cloud Security Principles**: Not documented

### Recommendations for government use

**Unclassified development (OFFICIAL)**:
- Conditional approval with careful configuration
- Not recommended for personal data or sensitive information

**Operational systems (OFFICIAL-SENSITIVE)**:
- Requires Enterprise tier with on-premises deployment
- Extensive additional controls and bespoke contractual terms needed

**Classified systems (SECRET, TOP SECRET)**:
- Standard service not suitable
- Mandatory cloud processing incompatible with classification requirements

### Key actions before procurement

1. Request SOC 2 report via Trust Centre
2. Verify UK GDPR compliance explicitly
3. Assess Cyber Essentials certification roadmap
4. Negotiate enhanced liability provisions and service level agreements
5. For Enterprise: Request architecture diagrams for on-premises deployment

## References

### Official documentation
- Junie overview: https://www.jetbrains.com/junie/
- Documentation hub: https://www.jetbrains.com/help/idea/junie.html
- Data protection: https://www.jetbrains.com/help/junie/data-protection.html

### Legal and privacy
- AI Service Terms: https://www.jetbrains.com/legal/docs/terms/jetbrains-ai-service/
- Privacy Notice: https://www.jetbrains.com/legal/docs/privacy/privacy/
- Data Processing Agreement: https://www.jetbrains.com/legal/dpa/

### Security and compliance
- Trust Centre: https://trust-center.jetbrains.com/
- SOC 2 announcement: https://blog.jetbrains.com/security/2024/02/jetbrains-has-received-its-soc2-audit-report/
- Security contact: security-compliance@jetbrains.com

### Data management
- AI data collection policy: https://www.jetbrains.com/help/ai/data-collection-and-use-policy.html
- Data retention: https://www.jetbrains.com/help/ai/data-retention.html
- Third-party processors: https://www.jetbrains.com/legal/docs/privacy/third-parties/