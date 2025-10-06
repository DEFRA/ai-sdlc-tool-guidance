# IntelliJ Junie security and compliance assessment for UK government

## Executive summary

**JetBrains Junie is an AI coding agent that poses significant data sovereignty concerns for UK government use.** The tool requires mandatory cloud processing through US-based third-party AI providers (OpenAI and Anthropic), with no option to restrict data to UK or EU jurisdictions under standard licensing. Whilst JetBrains demonstrates strong GDPR compliance and has achieved SOC 2 Type II certification, the service **lacks comprehensive audit logging capabilities and UK-specific security certifications** such as Cyber Essentials.

For standard AI Free, Pro, and Ultimate licence tiers, all code snippets and prompts are transmitted to external large language model providers with default retention periods of 7-30 days. **Enterprise customers can achieve air-gapped, UK-resident deployment through on-premises installation**, but this requires significant infrastructure investment and separate licensing arrangements.

**Recommendation for classified or sensitive UK government work: The standard service is not suitable.** Enterprise deployment with on-premises hosting may be viable for lower-classification work, subject to thorough security assessment and contractual guarantees.

---

## 1. Tool overview

### What is IntelliJ Junie

JetBrains Junie is an AI coding agent that autonomously plans and executes complex, multi-step programming tasks within JetBrains integrated development environments (IDEs). Unlike traditional AI coding assistants that provide suggestions, **Junie operates autonomously** - it can navigate project files, run code, execute terminal commands, and modify file systems based on natural language instructions from developers.

**Official website:** https://www.jetbrains.com/junie/

### Core functionality and operation

Junie integrates directly into the IDE and uses the IDE's native tools (code navigation, search, inspections) to:

- Analyse project structure and technology stack
- Create and edit multiple files simultaneously
- Execute tests and verify code changes
- Run terminal commands and git operations
- Report progress and provide execution plans before taking action

The agent operates in two modes: **Code mode** (default) where it makes changes to your codebase, and **Ask mode** where it provides information without modifications.

### Supported development environments

Junie is available as a plugin for:
- IntelliJ IDEA (Ultimate and Community editions, version 2024.3.2+ required)
- PyCharm Professional and Community (2024.3.2+)
- WebStorm, GoLand, PhpStorm (2024.3.2+)
- RubyMine, RustRover (2025.1+)
- Android Studio, CLion

The plugin supports Java, Kotlin, Python, JavaScript, TypeScript, Go, PHP, and Rust, with unofficial support for additional languages.

### Critical technical limitation: Cloud-only operation

**Junie requires continuous internet connectivity and operates exclusively in online mode.** All processing relies on external large language model (LLM) providers:

- **Default model:** GPT-5 by OpenAI (US-based)
- **Alternative models:** Claude Sonnet 3.7 and 4.0 by Anthropic (US-based)
- **No offline mode** with local models is currently available

Users can select their preferred model through IDE settings, but **cannot opt out of cloud processing whilst using the service**.

### Licensing and activation

Junie requires a JetBrains AI licence, available in four tiers:
- **AI Free:** Limited monthly quota, available with active IDE licences
- **AI Pro:** Higher quota for individual/organisational use
- **AI Ultimate:** Highest quota tier
- **AI Enterprise:** Includes organisation-wide administration, custom LLM providers, and on-premises deployment options

All licences are linked to JetBrains Accounts for authentication. New users receive a 30-day AI Pro trial. Usage is governed by quota (AI Credits) that resets monthly and regulates access to cloud-based LLM features.

---

## 2. Privacy settings and data controls

### Data transmitted to third parties

When using Junie, the following data is transmitted to third-party LLM providers:

- User prompts and natural language instructions
- Selected code snippets and file contents
- Project context (file types, frameworks, code structure)
- Additional context necessary for LLM processing

**JetBrains states it does not use this data for training AI models** without explicit user consent. However, third-party LLM providers (OpenAI and Anthropic) **may monitor inputs and outputs** to prevent violations of acceptable use policies, and may store this data for limited periods (7-30 days depending on provider).

**Critical concern:** JetBrains explicitly states that "neither the user nor JetBrains has control over this third-party data processing" once data is transmitted to LLM providers.

### Available privacy controls

**Project-level controls:**

1. **.aiignore file** - Specify files and folders that require explicit approval before Junie can access them. Note that file and folder names remain visible even when listed in .aiignore.

2. **Approved directory setting** - Designate a specific directory where Junie can modify files without confirmation. Files outside this directory require user approval.

3. **Action allowlist** - Control which terminal commands and external tools Junie can execute without approval. Supports regular expressions for command patterns.

4. **Brave mode** - When enabled, allows Junie to run terminal commands without explicit approval each time (less secure).

**Organisation-level controls (Enterprise tier only):**

- Administrators can enable or disable JetBrains AI for all users in the organisation
- Configure detailed data collection settings per profile
- Set usage limits and monthly AI Credits caps
- Connect custom LLM providers for on-premises deployment

**Settings documentation:**
- Project settings: https://www.jetbrains.com/help/junie/project-settings.html
- .aiignore configuration: https://www.jetbrains.com/help/junie/aiignore.html
- Action allowlist: https://www.jetbrains.com/help/junie/action-allowlist.html

### Data collection options

**Zero data retention (default):**
By default, JetBrains operates in "zero data retention" mode where inputs are sent directly to LLM providers and outputs returned to the IDE without persistent storage on JetBrains servers.

**Detailed data collection (opt-in only):**
Users can explicitly opt in to share:
- Full text of prompts and responses
- Complete code snippets in LLM interactions
- Retained for maximum 30 days
- Used only by JetBrains LLM development teams
- **Not used for training code generation models**

**Behavioural data:**
When enabled (disabled by default in release builds), JetBrains collects:
- Types of AI features used
- Acceptance rates for suggestions
- Performance metrics
- User feedback on quality
- Does **not** include personally identifiable data or source code

### Critical limitations for government use

**No options to:**
- Operate in offline mode or with local-only models (for Junie specifically)
- Disable data sharing with third-party LLM providers whilst using the service
- Configure data retention periods with third-party providers (standard licences)
- Select UK-only or EU-only data processing regions
- Disable telemetry separately from core functionality

**Geographic restrictions:** Access to Junie is restricted in certain countries due to limitations imposed by AI providers (OpenAI, Anthropic, Google).

---

## 3. Terms of use and privacy policy

### Terms of service

**Document:** JetBrains AI Service Terms of Use  
**URL:** https://www.jetbrains.com/legal/docs/terms/jetbrains-ai-service/  
**Version:** 2.0, effective 22 May 2024  
**Governing law:** Czech Republic  
**Entity:** JetBrains s.r.o. (Czech Republic)

**Key provisions relevant to government procurement:**

**Liability limitations:**
- Service provided "as is" with **no express warranties**
- Maximum liability limited to greater of $100 USD or amount paid in preceding 6 months
- No liability for indirect, incidental, special, consequential, or exemplary damages
- No warranty of merchantability, fitness for particular purpose, or non-infringement
- **Users solely responsible for evaluating accuracy and suitability** of AI-generated outputs

**Service continuity:**
- "Commercially reasonable efforts" only - no guaranteed service level agreements
- JetBrains may discontinue service with 30 days' notice
- Can terminate accounts for material breach, non-payment, security risks, or legal requirements
- 30-day cure period provided for most breaches

**Acceptable use:**
- Customer responsible for ensuring shared data complies with export control laws
- Prohibited: Illegal content, unauthorised access, reselling, security circumvention
- Personal data as input is **prohibited** under terms
- Customer bears sole responsibility for data sensitivity assessment

**Commentary:** The extensive liability limitations and lack of guaranteed service levels may not align with public sector requirements for critical systems. Government procurement should negotiate bespoke contractual terms with appropriate liability provisions and service level agreements.

**Additional terms:**
- Junie-specific terms: https://www.jetbrains.com/legal/docs/terms/jetbrains-junie/
- AI Acceptable Use Policy: https://www.jetbrains.com/legal/docs/terms/jetbrains-ai/acceptable-use/

### Privacy policy

**Document:** JetBrains Privacy Notice  
**URL:** https://www.jetbrains.com/legal/docs/privacy/privacy/  
**Data controllers:** JetBrains s.r.o. and associated companies (joint controllers)  
**Data Protection Officer:** dpo@jetbrains.com

**Key provisions:**

**Personal data collected:**
- Identifiers: name, address, IP address, online identifiers, telephone number
- Customer records: contact information, financial/payment information
- Commercial information: purchase history, product usage
- Internet activity: browsing history, interaction data
- Location data: physical location via IP address
- Inferences: user preferences, characteristics, behaviour profiles

**Legal bases for processing:**
- Performance of contract
- Legitimate interests (anti-piracy, evidence, marketing)
- Legal compliance
- Explicit consent (where required)

**Data sharing:**
JetBrains shares personal data with:
- Associated companies within JetBrains group
- Data processors (list at https://www.jetbrains.com/legal/docs/privacy/third-parties/)
- Third-party AI providers: OpenAI, Anthropic, Google, Amazon (list at https://www.jetbrains.com/legal/docs/terms/jetbrains-ai/service-providers/)
- Government bodies (legal obligations)
- Potential merger/acquisition parties

**GDPR compliance:**
JetBrains demonstrates strong GDPR compliance as an EU entity directly regulated by Czech and EU data protection law. The privacy policy comprehensively addresses:

- All data subject rights (access, rectification, erasure, restriction, portability, objection)
- Right to lodge complaints with supervisory authorities
- Clear legal bases for processing
- Standard Contractual Clauses for international transfers
- Designated Data Protection Officer
- Data Processing Agreement available at https://www.jetbrains.com/legal/dpa/

**UK considerations:** Whilst JetBrains' EU GDPR compliance provides a strong foundation, post-Brexit UK GDPR is a separate legal framework. The UK adequacy decision currently facilitates EU-UK data transfers, but government procurement should verify ongoing UK GDPR compliance explicitly.

**Data retention:**
- Data retained as long as necessary for stated purposes
- Legal and compliance requirements may extend retention
- Users can request deletion via privacy@jetbrains.com or JetBrains Account settings
- Pseudonymised records may remain after deletion

**Security measures documented:**
- Encryption in transit (TLS) and at rest (AES-256)
- Regular encryption key rotation
- Strict access controls
- Supplier risk assessment processes

**Additional documentation:**
- AI-specific data policy: https://www.jetbrains.com/help/ai/data-collection-and-use-policy.html
- Data retention details: https://www.jetbrains.com/help/ai/data-retention.html

---

## 4. Data management

### Server location and data residency

**Infrastructure providers:**
JetBrains AI services use **Amazon Web Services (AWS) and Google Cloud Platform** as core infrastructure layers.

**Geographic locations:**
- Servers located in **EU, US, and Asia**
- Specific data centre locations or countries not disclosed in public documentation
- For general JetBrains services, default location is EU
- **For JetBrains AI specifically, default storage location may differ** from EU

**Third-party LLM provider locations:**

| Provider | Headquarters | Data processing location | UK government restriction |
|----------|--------------|-------------------------|---------------------------|
| OpenAI | United States | Primarily US; some processing via Ireland subsidiary for EEA data | ⚠️ Data leaves UK/EU to US jurisdiction |
| Anthropic | United States | US-based operations | ⚠️ Data leaves UK/EU to US jurisdiction |
| Google Vertex AI | United States | Multi-region; can be configured for EU regions by enterprise customers | ⚠️ Requires enterprise configuration for EU residency |
| Amazon Bedrock | United States | Multi-region AWS infrastructure; configurable | ⚠️ Requires enterprise configuration for regional control |

**Data residency options by licence tier:**

**Standard licences (AI Free, Pro, Ultimate):**
- **No explicit data residency controls available**
- **No option to restrict processing to UK or EU only**
- Data transmitted to US-based third-party providers for all processing
- No ability to select geographic regions for data storage or processing

**Enterprise licence (AI Enterprise via IDE Services):**
- ✅ On-premises installation available for air-gapped environments
- ✅ Can connect on-premises models via Hugging Face
- ✅ Can configure Azure OpenAI, Google Vertex AI, or Amazon Bedrock with regional controls
- Requires separate enterprise licensing and infrastructure

**UK data sovereignty assessment:**

**Standard licences:** ❌ **FAIL** - Data leaves UK/EU jurisdiction to US providers with no opt-out

**Enterprise licence:** ⚠️ **CONDITIONAL PASS** - Only if deployed on-premises or configured with regional LLM providers through bespoke enterprise arrangements

**Critical concern:** The US CLOUD Act may compel US-based providers to disclose data to US authorities, regardless of where data is physically stored. This poses sovereignty risks for sensitive UK government data.

### Data in transit

**Encryption standard:**
- **Transport Layer Security (TLS)** protocol used for all data transmission
- Described as "up-to-date TLS protocol"
- **Specific TLS version (1.2 vs 1.3) not explicitly documented** by JetBrains
- OpenAI documentation confirms TLS 1.2+ for their services
- Anthropic and Google confirm TLS encryption but versions not specified

**Assessment:** ✅ Industry-standard encryption in transit  
**UK government restriction:** ⚠️ Lack of explicit TLS version commitment; government should require TLS 1.3 minimum for new implementations

**Additional transport security:**
- No explicit mention of certificate pinning
- No documentation of additional transport security measures beyond TLS

### Data at rest

**Encryption method:**
- **AES-256 encryption** for data stored on JetBrains servers
- Described as "strong, up-to-date encryption algorithms"
- Encryption keys regularly rotated
- Access to encryption keys strictly limited

**Storage locations:**

**JetBrains servers:**
- Semantic code embeddings (numerical representations of code structure) stored on JetBrains servers within AWS/Google Cloud infrastructure
- Storage described as "temporary, strictly for indexing purposes"
- **Specific storage duration not documented**

**Third-party LLM providers:**
All major providers use AES-256 encryption at rest:
- OpenAI: AES-256
- Anthropic: AES-256
- Google Vertex AI: AES-256 (Google Cloud standard)

**Assessment:** ✅ Industry-standard AES-256 encryption at rest  
**UK government restriction:** ⚠️ Storage duration for semantic indexing undefined; unclear data lifecycle

### Data retention

**JetBrains retention policy:**

**Default (zero data retention mode):**
- **No persistent storage** on JetBrains servers by default
- Inputs sent directly to LLM provider
- Outputs returned directly to user IDE
- ✅ True zero data retention for JetBrains infrastructure

**With detailed data collection opt-in:**
- **Maximum 30 days** retention on JetBrains servers
- Includes full text of inputs, outputs, and code snippets
- Access restricted to JetBrains LLM development teams only
- **Not used for training AI models**

**Semantic code indexing:**
- Code embeddings stored "temporarily"
- **Specific retention period not documented**
- Private repository indexes restricted to repository owner
- Enterprise indexes accessible within organisation only

**Behavioural data:**
- Usage statistics, feature acceptance rates, performance data
- **Retention period not explicitly documented**
- Does not include personally identifiable data or source code

**Third-party LLM provider retention:**

| Provider | Default retention | Zero data retention option | UK government restriction |
|----------|------------------|---------------------------|---------------------------|
| OpenAI | 30 days (abuse monitoring) | ✅ Available for enterprise customers by request | ⚠️ Requires separate ZDR negotiation; not automatic |
| Anthropic | 7 days (changing from 30 days, effective 15 Sept 2025) | ✅ Available for approved enterprise API customers | ⚠️ Trust/safety data retained up to 7 years regardless |
| Google Vertex AI | 24 hours caching by default | ✅ Achievable by disabling caching and opting out of abuse monitoring | ⚠️ Requires enterprise configuration |

**Critical findings:**

- ❌ **Default 7-30 day retention by third-party providers** even with JetBrains zero data retention
- ❌ **Zero data retention with LLM providers requires separate enterprise arrangements** not included in standard licences
- ❌ **Trust and safety flagged content** may be retained by Anthropic for up to 7 years
- ❌ **No documented differences in retention by licence tier** (Free, Pro, Ultimate, Enterprise follow same JetBrains policy)
- ❌ **No clear data deletion procedures** for user-initiated deletion requests

**UK government restriction:** Standard licences do not provide adequate data retention controls. Enterprise agreements with verified zero data retention from all providers would be required as minimum for government use.

### Data retention by plan/tier

**Documented retention policies apply equally across all licence tiers:**
- AI Free
- AI Pro
- AI Ultimate
- AI Enterprise

The JetBrains zero data retention policy is **consistent across all tiers**. The primary difference is quota (AI Credits) rather than data handling practices.

**Enterprise tier advantages:**
Whilst retention policy is the same, AI Enterprise customers can:
- Negotiate separate zero data retention agreements directly with LLM providers
- Deploy on-premises to avoid external data transmission entirely
- Configure custom LLM providers with bespoke data handling terms

---

## 5. Audit logging

### Critical finding: No comprehensive audit logging

**Extensive review of official documentation found no evidence of dedicated audit logging capabilities** for tracking Junie activities, user actions, or code modifications for compliance or security monitoring purposes.

### Available monitoring capabilities

**Quota and usage tracking:**
- Users can view AI Credits consumption in Junie tool window (Options → Licence Info)
- Organisation administrators can track top-up AI Credits usage in JetBrains Account
- **Limitation:** Tracks resource consumption only, not detailed activity logs

**In-session activity visibility:**
During active Junie sessions, users can see:
- Which files Junie adds or edits
- Code changes in real-time diff viewer
- List of changed/added files in "Done" panel after task completion
- Terminal command outputs in Junie's terminal
- Execution plan before action is taken

**Limitation:** This provides transparency during sessions but **not persistent audit trails** for retrospective review or compliance verification.

**Enterprise monitoring (AI Enterprise tier):**
Administrators can:
- Set usage limits per user or profile
- Track AI Credits consumption
- Configure detailed data collection settings
- **No evidence of comprehensive audit logging** for security events or user activities

### Audit logging gaps

The following audit capabilities are **not documented:**

- ❌ Persistent logs of Junie activities and actions taken
- ❌ Activity logging accessible to administrators
- ❌ User action tracking for compliance purposes
- ❌ Event logging for security monitoring
- ❌ Git operation audit trails specific to Junie
- ❌ Terminal command execution logs with timestamps
- ❌ File system modification audit records
- ❌ User authentication and access logs for Junie features
- ❌ Failed action attempt logging
- ❌ Compliance logging for regulatory requirements

**UK government restriction:** ❌ **CRITICAL GAP** - Lack of comprehensive audit logging makes the tool **unsuitable for environments requiring audit trails** for security compliance, incident investigation, or regulatory requirements such as Government Security Classifications Policy.

### Recommendations

For government use requiring audit trails:
1. Implement external monitoring through IDE or system-level logging
2. Use version control commit messages to track Junie-generated changes
3. Require manual review and approval of all Junie actions before acceptance
4. Consider third-party audit logging solutions that monitor IDE activity
5. Request audit logging features in enterprise negotiations with JetBrains

---

## 6. Access controls

### User authentication and account management

**Authentication:**
- Requires JetBrains Account for licence activation and use
- Authentication handled through JetBrains Account system
- Licence linked to individual user accounts
- No multi-factor authentication (MFA) explicitly documented for Junie access

**Account types:**
- Individual user accounts
- Organisation accounts (for enterprise customers)
- Licence assignment managed through JetBrains Account Administration portal

### Licence tiers and access levels

Four licence tiers with different quota allocations:

| Tier | Access level | Primary difference |
|------|-------------|-------------------|
| AI Free | Limited quota | Restricted AI Credits per 30-day cycle |
| AI Pro | Higher quota | Increased AI Credits allocation |
| AI Ultimate | Highest quota | Maximum AI Credits allocation |
| AI Enterprise | Enterprise features | Organisation administration, custom LLM providers, on-premises options |

**Key distinction:** Tiers primarily differ in quota size (AI Credits for cloud model access) rather than feature access or permission levels.

### Organisation-level controls

**For AI Enterprise customers:**

Administrators can:
- **Enable or disable JetBrains AI** for all users in the organisation through JetBrains Account Administration
- Set usage limits and monthly AI Credits caps per user or profile
- Configure which AI providers are available (OpenAI, Anthropic, custom providers)
- Control detailed data collection per profile
- Make Junie available in selected profiles only
- Track quota consumption across the organisation

**Administration portal:** JetBrains Account Administration  
**Documentation:** https://www.jetbrains.com/help/ide-services/manage-aie.html

**Limitation:** No granular role-based access control (RBAC) within Junie itself beyond enable/disable and profile-based availability.

### Project-level access controls

**Approved directory:**
- Specify a directory where Junie can modify files without confirmation
- Files outside this directory require explicit user approval before modification
- Configured per project in Junie settings
- Can be version-controlled and shared across teams

**.aiignore file:**
- List files and folders requiring explicit approval before Junie can view or edit
- Similar concept to .gitignore
- **Limitation:** File and folder names remain visible even when in .aiignore
- Requires explicit user confirmation before access
- Can be version-controlled and shared with team

**Documentation:**
- Project settings: https://www.jetbrains.com/help/junie/project-settings.html
- .aiignore: https://www.jetbrains.com/help/junie/aiignore.html

### Action-level controls

**Action allowlist:**
- Control which **terminal commands** Junie can execute without user approval
- Support for regular expressions (RegEx) to define command patterns
- Control Model Context Protocol (MCP) tool execution permissions
- Other action types can be authorised without approval

**Default behaviour:**
Junie requires user approval for:
- Running terminal commands
- Executing MCP tools (external integrations)
- Other potentially risky actions

**Brave mode:**
When enabled, Junie can execute terminal commands without explicit approval each time (less secure).

**Documentation:** https://www.jetbrains.com/help/junie/action-allowlist.html

### Git commit permissions

**No specific git permission controls documented.**

Junie can execute git commands as part of task execution, including:
- git add
- git commit
- git push (if configured)
- Other git operations

**Control mechanism:** Git command authorisation follows general Action Allowlist settings. Organisations can restrict git commands through allowlist regular expressions.

**Security consideration:** Without explicit git controls, Junie could potentially commit or push code changes if granted broad terminal permissions. Government teams should:
- Use Action Allowlist to restrict git commands
- Require manual review of all changes before committing
- Configure repository-level protections (branch protection, required reviews)

### Role-based access controls

**Limited RBAC capabilities:**

Available controls:
- Organisation administrators can enable/disable for all users
- AI Enterprise tier provides profile-based configuration
- No documented granular role-based permissions within Junie itself
- User permissions primarily determined by licence tier and organisation settings

**Not available:**
- ❌ Granular permission levels (viewer, editor, administrator within Junie)
- ❌ Feature-level access controls (e.g., allow Code mode but not terminal access)
- ❌ Repository-specific permissions
- ❌ Time-based access controls
- ❌ IP-based access restrictions

### Multi-user and team controls

**Shared configuration:**
Teams can version-control and share:
- **.junie/guidelines.md** - Project-specific coding standards and guidelines that Junie will follow
- **.aiignore** - Shared file/folder access restrictions
- **MCP configurations** - External tool integration settings (.junie/mcp.json)

These configurations enable consistent behaviour across team members whilst maintaining individual user authentication.

**Documentation:** https://www.jetbrains.com/help/junie/customize-guidelines.html

### UK government restrictions

**Critical gaps for government use:**

- ❌ **No multi-factor authentication** explicitly documented
- ❌ **No granular RBAC** beyond enable/disable
- ❌ **No integration with government identity providers** (Active Directory, GSuite, etc.) documented
- ❌ **No git-specific permission controls** beyond general command allowlists
- ❌ **No network-level access controls** or IP whitelisting
- ❌ **No session timeout or inactivity controls** documented
- ❌ **No privileged access management** for sensitive operations

**Recommendations:**
- Implement network-level controls to restrict Junie endpoints if needed
- Use git repository-level protections rather than relying on Junie controls
- Require manual review and approval of all Junie outputs before committing to repositories
- Consider least-privilege approach: disable Junie for users handling classified information

---

## 7. Compliance and regulatory requirements

### Confirmed certifications and compliance

**SOC 2 Type II (Confirmed ✅)**

JetBrains has achieved SOC 2 Type II certification, audited against all five Trust Service Criteria:
- Security
- Availability
- Processing Integrity
- Confidentiality
- Privacy

**Audit details:**
- Auditor: External auditor per AICPA requirements
- Most recent audit: February 2024
- Report access: Available via JetBrains Trust Centre (requires NDA)

**Scope (2023 audit):**
The SOC 2 audit covered multiple JetBrains products including:
- YouTrack
- TeamCity
- Space
- Datalore
- Remote Development
- Code With Me
- Fleet
- JetBrains IDEs
- .NET & Visual Studio Tools

**Limitation:** Junie and JetBrains AI services were **not explicitly listed in the 2023 audit scope**. JetBrains plans to expand scope in future audits.

**Access to report:**
- Available via JetBrains Trust Centre: https://trust-center.jetbrains.com/
- Requires execution of Non-Disclosure Agreement
- Includes penetration testing reports
- Real-time security control status monitoring

**Source:** https://blog.jetbrains.com/security/2024/02/jetbrains-has-received-its-soc2-audit-report/

**GDPR compliance (Confirmed ✅)**

JetBrains demonstrates comprehensive GDPR compliance as an EU entity based in Czech Republic and directly regulated by EU data protection law.

**Compliance measures:**
- Designated Data Protection Officer (dpo@jetbrains.com)
- Comprehensive Data Processing Agreement available
- Standard Contractual Clauses for international data transfers
- Full implementation of data subject rights
- Regular compliance audits
- Clear legal bases for all processing activities
- Privacy by Design principles

**UK considerations:**
Post-Brexit, UK GDPR is a separate legal framework from EU GDPR. Whilst EU GDPR compliance provides strong foundation, and UK adequacy decision currently facilitates EU-UK transfers, government procurement should verify:
- Explicit UK GDPR compliance statement
- Awareness of UK Information Commissioner's Office guidance
- Monitoring of UK regulatory divergence from EU GDPR

**Documentation:**
- Privacy Policy: https://www.jetbrains.com/legal/docs/privacy/privacy/
- Data Processing Agreement: https://www.jetbrains.com/legal/dpa/
- Data Protection Officer: dpo@jetbrains.com

**Infrastructure provider certifications (Inherited)**

JetBrains uses AWS and Google Cloud Platform, which maintain:
- ISO 27001 (Information Security Management)
- ISO 27017 (Cloud Security)
- ISO 27018 (Cloud Privacy)
- PCI DSS Level 1
- SOC 1, SOC 2, SOC 3

**Important limitation:** These are infrastructure provider certifications, not JetBrains certifications. JetBrains benefits from secure infrastructure but **does not hold independent ISO 27001 certification**.

### UK-specific standards: Not certified

**Cyber Essentials:** ❌ No evidence of certification  
**Cyber Essentials Plus:** ❌ No evidence of certification  
**UK Government Security Classifications:** ❌ Not documented  
**NCSC Cloud Security Principles compliance:** ❌ Not explicitly stated

**Assessment:** The absence of Cyber Essentials certification is notable for UK government procurement, as this is often a minimum requirement for handling UK government data, particularly for contracts involving personal data or systems connected to government networks.

### International standards: Not independently certified

**ISO 27001 (Information Security Management):** ❌ JetBrains not directly certified (relies on AWS/Google Cloud certification)  
**ISO 27017 (Cloud Security):** ❌ Not documented  
**ISO 27018 (Cloud Privacy):** ❌ Not documented  
**ISO 9001 (Quality Management):** ❌ Not documented

### Security measures documented

Beyond formal certifications, JetBrains documents these security practices:

**Encryption:**
- TLS in transit
- AES-256 at rest
- Regular encryption key rotation

**Access controls:**
- Strict access controls
- Role-based access (infrastructure level)
- Limited access to encryption keys

**Security testing:**
- Penetration testing (reports available via Trust Centre)
- Vulnerability management programme
- Regular security updates

**Supplier management:**
- Risk assessment process for sub-processors
- Contractual security requirements for third parties
- List of sub-processors published and maintained

**Security contact:**
- Email: security-compliance@jetbrains.com
- Trust Centre: https://trust-center.jetbrains.com/

### Third-party LLM provider compliance

**OpenAI:**
- SOC 2 Type II certified
- ISO 27001 certified
- GDPR compliant
- Not trained on API customer data
- 30-day retention for abuse monitoring (ZDR available for enterprise)

**Anthropic:**
- SOC 2 Type II certified
- GDPR compliant
- Not trained on customer data without consent
- 7-day retention (changing from 30 days, September 2025)
- Trust and safety data retained up to 7 years

**Google Vertex AI:**
- ISO 27001, ISO 27017, ISO 27018 certified
- SOC 2 Type II certified
- GDPR compliant
- Not used for training without permission
- 24-hour default caching (can be disabled)

**Note:** Government data sent to these providers is subject to **their** compliance frameworks and policies, not solely JetBrains' frameworks.

### Compliance gaps for UK government use

**Critical gaps:**

1. **No UK Cyber Essentials certification** - Often minimum requirement for government contracts
2. **No direct ISO 27001 certification** - Infrastructure-only, not JetBrains entity certification
3. **No NCSC Cloud Security Principles assessment** publicly available
4. **No explicit UK Government Security Classifications** handling capability
5. **No FedRAMP or government-specific certifications**
6. **Junie not included in current SOC 2 scope** - Future inclusion planned but not confirmed

**Export control considerations:**
- JetBrains based in Czech Republic (EU entity)
- Customer responsible for ensuring data compliance with export control laws
- No documentation of compatibility with UK Official Secrets Act
- No cleared personnel for handling classified UK government information

### Recommendations for government procurement

**For low-risk, unclassified development work:**
1. Verify Junie inclusion in future SOC 2 audits
2. Request explicit UK GDPR compliance statement
3. Assess whether lack of Cyber Essentials is acceptable for your use case

**For medium-risk or operational systems:**
1. Request bespoke contractual terms with enhanced liability provisions
2. Require evidence of Cyber Essentials or commitment to certification
3. Conduct independent security assessment
4. Verify third-party LLM provider compliance meets your requirements
5. Consider on-premises Enterprise deployment

**For high-risk or classified systems:**
1. Standard service not recommended without significant enhancements
2. Enterprise on-premises deployment required as minimum
3. Request government-specific security assessment
4. Negotiate bespoke terms including:
    - Enhanced liability provisions
    - Service level agreements with penalties
    - Guaranteed audit logging capabilities
    - UK-specific data residency guarantees
    - Incident response and breach notification procedures
    - Right to audit

**Contact for compliance enquiries:**
- Security and compliance: security-compliance@jetbrains.com
- Data protection: dpo@jetbrains.com
- Trust Centre: https://trust-center.jetbrains.com/

---

## Summary assessment

### Strengths

✅ Strong GDPR compliance framework with comprehensive data subject rights  
✅ SOC 2 Type II certification demonstrates security maturity  
✅ Transparent data processing documentation  
✅ Zero data retention by default on JetBrains infrastructure  
✅ User control over detailed data collection (opt-in only)  
✅ Contractual commitment not to use customer data for AI training  
✅ Project-level access controls (.aiignore, approved directories)  
✅ Clear acceptable use policies  
✅ Enterprise options for on-premises deployment

### Critical concerns for UK government use

❌ **Mandatory cloud processing** - No offline mode; all data sent to US-based third-party LLM providers  
❌ **Data sovereignty** - Data leaves UK/EU jurisdiction under standard licences  
❌ **No comprehensive audit logging** - Cannot track activities for compliance or security monitoring  
❌ **No UK Cyber Essentials certification** - Often minimum requirement for government contracts  
❌ **No direct ISO 27001 certification** - Relies on infrastructure provider certifications only  
❌ **Limited liability** - Maximum $100 or 6-month payment cap may be insufficient  
❌ **Third-party data retention** - 7-30 days by LLM providers even with JetBrains ZDR  
❌ **No guaranteed service levels** - "Commercially reasonable efforts" only  
❌ **Limited access controls** - No granular RBAC or git-specific permissions  
❌ **US CLOUD Act implications** - US-based providers may be compelled to disclose data

### Suitability assessment by use case

**Unclassified development and testing (OFFICIAL):**  
⚠️ **Conditional approval** with careful configuration:
- Enable zero data retention mode
- Use .aiignore for any sensitive files
- Require manual review of all AI-generated code
- Verify acceptable use policy compliance
- Assess whether lack of audit logging is acceptable
- **Not recommended for personal data or sensitive information**

**Operational systems (OFFICIAL-SENSITIVE):**  
⚠️ **Requires enhanced due diligence:**
- Consider AI Enterprise with on-premises deployment
- Negotiate bespoke contractual terms
- Verify third-party LLM provider arrangements
- Implement compensating controls for audit logging gaps
- Conduct independent security assessment
- **Not recommended without Enterprise tier and extensive additional controls**

**Classified systems (SECRET, TOP SECRET):**  
❌ **Standard service not suitable:**
- Mandatory third-party cloud processing incompatible with classification requirements
- Lack of comprehensive audit logging insufficient for compliance
- No UK government-specific security certifications
- Data sovereignty concerns cannot be adequately mitigated
- **Only Enterprise on-premises deployment could potentially be considered** after thorough security assessment and assurance that no data leaves government-controlled infrastructure

### Recommended actions

**Before procurement:**
1. Request SOC 2 report via Trust Centre (requires NDA execution)
2. Verify Junie's inclusion in current or planned SOC 2 audit scope
3. Request explicit UK GDPR compliance statement and monitoring approach for UK regulatory divergence
4. Assess Cyber Essentials certification roadmap
5. For Enterprise consideration: Request architecture diagrams for on-premises deployment

**During procurement:**
1. Negotiate bespoke terms addressing:
    - Enhanced liability provisions appropriate for government use
    - Service level agreements with clear uptime guarantees and remedies
    - Audit logging capabilities or timeline for implementation
    - Data residency guarantees for UK/EU processing
    - Incident response and breach notification procedures meeting UK government requirements
2. Clarify exit strategy and data deletion procedures
3. Establish regular compliance review cadence
4. Define acceptable use boundaries for your organisation

**After procurement:**
1. Implement network-level monitoring and controls
2. Configure strict Action Allowlists for terminal commands
3. Use .aiignore files extensively for sensitive paths
4. Require code review for all AI-generated code before merging
5. Track Junie usage through version control commit messages
6. Regular security reviews and compliance audits
7. Monitor for changes to third-party LLM provider policies

---

## References

### Official JetBrains documentation

1. Junie overview: https://www.jetbrains.com/junie/
2. Getting started with Junie: https://www.jetbrains.com/help/junie/get-started-with-junie.html
3. Junie documentation hub: https://www.jetbrains.com/help/idea/junie.html
4. IDE compatibility: https://www.jetbrains.com/help/junie/ide-compatibility.html
5. Installation guide: https://www.jetbrains.com/help/junie/install-junie.html
6. Data protection: https://www.jetbrains.com/help/junie/data-protection.html
7. Licensing and subscriptions: https://www.jetbrains.com/help/junie/licensing-and-subscriptions.html
8. Project settings: https://www.jetbrains.com/help/junie/project-settings.html
9. .aiignore configuration: https://www.jetbrains.com/help/junie/aiignore.html
10. Action allowlist: https://www.jetbrains.com/help/junie/action-allowlist.html
11. Customise guidelines: https://www.jetbrains.com/help/junie/customize-guidelines.html
12. Model selection: https://www.jetbrains.com/help/junie/models.html
13. Code mode: https://www.jetbrains.com/help/junie/code-mode.html
14. Model Context Protocol: https://www.jetbrains.com/help/junie/model-context-protocol-mcp.html
15. JetBrains Marketplace plugin page: https://plugins.jetbrains.com/plugin/26104-jetbrains-junie

### Legal and privacy documentation

16. JetBrains AI Service Terms of Use: https://www.jetbrains.com/legal/docs/terms/jetbrains-ai-service/
17. JetBrains Junie Terms: https://www.jetbrains.com/legal/docs/terms/jetbrains-junie/
18. Privacy Notice: https://www.jetbrains.com/legal/docs/privacy/privacy/
19. Data Processing Agreement: https://www.jetbrains.com/legal/dpa/
20. Acceptable Use Policy: https://www.jetbrains.com/legal/docs/terms/jetbrains-ai/acceptable-use/
21. AI Service Providers list: https://www.jetbrains.com/legal/docs/terms/jetbrains-ai/service-providers/
22. Third-party sub-processors: https://www.jetbrains.com/legal/docs/privacy/third-parties/

### Data management and privacy

23. AI data collection and use policy: https://www.jetbrains.com/help/ai/data-collection-and-use-policy.html
24. Data retention: https://www.jetbrains.com/help/ai/data-retention.html
25. JetBrains AI FAQ: https://lp.jetbrains.com/ai-ides-faq/

### Enterprise and administration

26. Manage AI Enterprise: https://www.jetbrains.com/help/ide-services/manage-aie.html
27. Enable or disable JetBrains AI for organisation: https://sales.jetbrains.com/hc/en-gb/articles/14753675807506-Enable-or-disable-JetBrains-AI-for-all-users-in-your-organization

### Security and compliance

28. Trust Centre: https://trust-center.jetbrains.com/
29. SOC 2 audit announcement: https://blog.jetbrains.com/security/2024/02/jetbrains-has-received-its-soc2-audit-report/
30. Security contact: security-compliance@jetbrains.com
31. Data Protection Officer: dpo@jetbrains.com

### Additional resources

32. Junie playbook for IntelliJ IDEA: https://www.jetbrains.com/guide/ai/article/junie/intellij-idea/
33. Junie features blog: https://blog.jetbrains.com/junie/2025/07/the-agentic-ai-era-at-jetbrains-is-here/
34. Kotlin development with Junie: https://blog.jetbrains.com/kotlin/2025/04/smarter-kotlin-development-with-jetbrains-ai-junie-and-ai-assistant-in-your-ide/

### Third-party LLM provider documentation

35. OpenAI Enterprise Privacy: https://openai.com/enterprise-privacy/
36. OpenAI Platform documentation: https://platform.openai.com/docs/guides/your-data
37. Anthropic Privacy Centre: https://privacy.claude.com/en/articles/7996866-how-long-do-you-store-my-organization-s-data
38. Anthropic data usage documentation: https://docs.claude.com/en/docs/claude-code/data-usage
39. Google Vertex AI data governance: https://cloud.google.com/vertex-ai/generative-ai/docs/data-governance