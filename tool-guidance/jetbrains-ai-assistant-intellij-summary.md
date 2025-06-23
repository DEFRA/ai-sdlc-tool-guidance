# JetBrains AI Assistant for IntelliJ IDEA - Summary

This summary covers the key points from the [detailed guide](jetbrains-ai-assistant-intellij-detailed.md). Use it to understand how JetBrains AI Assistant can work in government environments.

## What JetBrains AI Assistant does

JetBrains AI Assistant is an AI-powered development tool integrated across JetBrains IDEs, including IntelliJ IDEA. The assistant uses large language models (LLMs) to help developers with code generation, intelligent coding assistance, code explanations, documentation writing, and refactoring tasks.

The tool works as an integrated pair programmer within the IDE interface, allowing you to interact through chat or invoke AI actions directly in the editor. It can explain selected code snippets, generate unit tests, suggest improvements, create commit messages, and help debug errors.

**Licensing options:**
- **AI Free**: Core features with unlimited local code completion and a one-time limited quota of cloud AI queries (does not renew monthly)
- **AI Pro and AI Ultimate**: Higher monthly allowances for cloud AI queries, included with certain JetBrains subscriptions
- **AI Enterprise**: Highest usage limits plus enterprise features like user access management and custom/on-premises AI models

The tool requires a valid JetBrains IDE licence and JetBrains Account to access any AI features.

## Privacy controls

JetBrains provides comprehensive privacy controls with data sharing set to opt-in by default. In released versions of the IDE, detailed data collection is disabled by default.

**Two levels of data collection:**

**Behavioural data**: High-level usage metrics such as which AI features are used and acceptance rates for suggestions. This does not include source code or personal content and is governed by the IDE's general data sharing setting under *Help → Data Sharing*. You can disable this anonymous usage reporting.

**Detailed data**: Full text of prompts and AI responses, including code snippets. This is not collected or stored by JetBrains unless you explicitly opt in via IDE prompts or settings. By default, code and queries go directly to the LLM provider without being saved on JetBrains' servers.

You can operate the AI Assistant in "zero-data-retention" mode by maintaining default settings, ensuring no conversation or code content is persistently logged by JetBrains. These privacy choices can be reviewed and revoked at any time through IDE settings.

## Terms of use and privacy policy

Before using the AI Assistant, you must agree to the JetBrains AI Terms of Service. Key provisions relevant to government use include:

**Data processing responsibility**: The service sends prompts and context files to third-party LLM providers. JetBrains acts as an intermediary and imposes contractual obligations on providers to protect your data. You remain responsible for choosing which files or code to share with the AI.

**Ownership rights**: You retain ownership of your code and data. AI-generated outputs are considered your data, with no rights claimed by JetBrains over code or text suggestions.

**Training restrictions**: Both JetBrains and its AI subcontractors agree not to use your code or prompts for training AI models without permission. Third-party LLMs are configured not to learn from API inputs.

**Confidentiality**: JetBrains commits to keeping inputs and outputs confidential, using them only to provide the service. Third-party providers are bound by similar confidentiality obligations.

**User responsibility**: You must review and validate AI outputs before use, as suggestions may be incorrect or inappropriate. JetBrains disclaims liability for problems arising from uncritical use of AI output.

The JetBrains Privacy Policy confirms GDPR compliance and data processing in accordance with applicable laws. A Data Processing Agreement (DPA) is available for customers requiring formal compliance documentation.

## Where your data goes

### Multi-regional processing

JetBrains is an EU-based company headquartered in Prague, Czech Republic. By default, your data routes through servers in the EU, specifically AWS data centres in Ireland hosting JetBrains' "IDE Services" cloud infrastructure.

However, requests then reach third-party AI providers, which may be located outside Europe:

- **OpenAI (GPT models)**: Data processed in the United States with zero-data-retention mode
- **Anthropic (Claude models)**: Processed in the United States with no-retention policy
- **Google (PaLM/Gemini models)**: Multi-region processing (EU, US, and Asia data centres depending on availability)
- **Amazon Bedrock**: Regional selection available, primarily for enterprise users

**For the default cloud AI providers, data will leave the UK/EU in many cases.** Appropriate safeguards are in place via JetBrains' agreements using standard contractual clauses for data transfer.

The AI Enterprise plan can address residency concerns by allowing organisations to self-host parts of the AI service and use custom LLM endpoints, potentially keeping data within chosen jurisdictions.

### Data protection in transit

All data in transit is encrypted using modern TLS encryption. Communications between the IDE, JetBrains servers, and AI providers use HTTPS connections. JetBrains uses up-to-date TLS protocols and regularly rotates encryption keys.

Source code and queries are never transmitted in plaintext over the internet. The TLS 1.2/1.3 encryption level meets typical PSN/GovConnect requirements for confidentiality in transit.

Network administrators will need to allow IDE traffic to `*.jetbrains.com` and relevant cloud endpoints over port 443.

### Data protection at rest

By default, JetBrains AI is designed to avoid storing your code or prompts at rest. The service does not persistently store code or query data on its servers unless you opt in to detailed data collection.

In zero-retention mode (the default), data at rest on JetBrains' side is limited to temporary memory and short-term caches necessary to process requests, which are not written to long-term storage.

If you opt in to detailed data collection, JetBrains temporarily stores prompts and responses on EU servers with strong encryption at rest (AES-256 or similar) and restricted access.

**Third-party LLM providers** are contracted to not store or use data beyond immediate requests. Providers support zero-data retention, meaning your code is held in memory to generate responses and then discarded.

**Data retention period**: If detailed data collection is enabled, JetBrains stores interaction content for no longer than 30 days before deletion. Otherwise, no AI interaction data is retained on disk.

## Audit logs

Audit logging capabilities in the AI Assistant are limited. The service does not provide end-users or administrators with detailed audit logs of AI queries and responses, primarily because it does not persist this data by default.

**Available logging:**
- You can see current session history in the IDE chat window, but this is not saved once the session closes
- Usage metrics are collected for billing and monitoring (number of requests, tokens used per account)
- No native feature exists to review "who queried what" in terms of content

**Enterprise considerations:**
- AI Enterprise plan offers more potential for custom logging
- Organisations could configure on-premises LLM providers to log requests internally if required
- JetBrains may provide usage statistics upon request, though not content logs

JetBrains reserves the right to review content if necessary for legal compliance or abuse prevention, but this is not a customer-facing audit tool.

**Implication**: If audit logging of AI usage is required, the current free/pro service may not meet this need out-of-the-box. Organisations may need to implement policy-based documentation or consider the Enterprise setup for enhanced logging control.

## Access controls

Access to JetBrains AI Assistant is controlled through JetBrains Accounts and licence entitlements. Only users with active IDE licences can use the AI service. IntelliJ IDEA Community Edition users are not eligible for the AI service.

**Organisational control:**
- JetBrains Account for Organisations provides an admin portal for licence seat assignment
- AI Pro/Ultimate licences can be assigned or revoked for specific users
- AI Enterprise plan includes user access management features with single sign-on integration
- Enterprise plans support organisation-wide policies and restrictions on model providers

**Privilege limitations:**
- AI Assistant operates within your existing IDE permissions
- Cannot access files not already opened by you
- All code changes occur locally and require your confirmation
- Cannot automatically commit to version control or execute arbitrary system commands
- No independent ability to access resources beyond the IDE context

**Administrative controls:**
- Access can be controlled via licence management and network policy
- Organisations can block JetBrains AI domains if necessary
- Enterprise version allows integration with corporate identity management

## Compliance and regulation

JetBrains has designed the AI Assistant with major compliance considerations in mind, particularly concerning data protection and information security.

**GDPR / UK Data Protection Act:**
- JetBrains fully complies with GDPR as an EU-based company
- Data transfers outside the EU use European Commission adequacy mechanisms or Standard Contractual Clauses
- Data Processing Agreements available for UK government entities to satisfy UK GDPR requirements

**Data security standards:**
- Comprehensive security programme with industry-standard practices
- Use of ISO 27001-compliant data centres (AWS, GCP)
- Implementation of least privilege access, encryption in transit and at rest
- Regular security reviews and supplier risk assessments

**Privacy and ethics:**
- Explicit commitment not to use customer code for training AI models
- User control over data sharing and processing
- Transparency in data handling practices
- Focus on minimising data at rest and user consent

**Regulatory compliance:**
- Export control law compliance required
- Service not available in sanctioned regions
- Standard restrictions on processing sanctioned data
- UK is fully supported for service usage

**Key considerations for government adoption:**
1. EU data processing with some US transit must be acceptable for the use case
2. Zero-retention mode should meet data protection requirements
3. Limited audit logging may not meet all compliance needs
4. Enterprise plan may be necessary for enhanced control and on-premises options
5. Developers must understand terms and follow internal guidelines for sensitive code

## What to do next

1. Review JetBrains' AI Terms of Service and Privacy Policy with your legal team
2. Decide if EU data processing with some US transit is acceptable for your use case
3. Check if zero-retention mode meets your data protection requirements
4. Consider whether the limited audit logging meets your compliance needs
5. Assess if the Enterprise plan is needed for enhanced control and on-premises options

## References

- JetBrains, **JetBrains AI Terms of Service** (v2.0, effective May 22, 2024)
- JetBrains, **Privacy Policy** (Version 3.0, July 2024)
- JetBrains, **Third-Party Services for JetBrains AI** (April 2025)
- JetBrains, **JetBrains AI Documentation – AI Service Licensing** (June 2025)
- JetBrains, **JetBrains AI Documentation – About AI Assistant** (April 2025)
- JetBrains, **Data Collection and Use Policy** (April 2025)
- JetBrains, **Data Retention FAQ** (April 2025)
- InfoWorld (via Major Digest), **"JetBrains IDEs now include AI tools by subscription"** (18 April 2025)