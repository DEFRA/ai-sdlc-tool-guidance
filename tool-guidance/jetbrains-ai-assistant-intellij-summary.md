# JetBrains AI Assistant for IntelliJ IDEA

**Approval status:** Under review - this tool is not currently approved for use. We are reviewing it for potential approval, but cannot commit to if or when this might happen.

This summary covers the key points from the [detailed guide](jetbrains-ai-assistant-intellij-detailed.md).

## Tool Overview

JetBrains AI Assistant helps you write code faster in IntelliJ IDEA and other JetBrains IDEs. It suggests code, explains existing code, writes tests, and helps debug problems.

**Licence options:**
- **AI Free**: Basic features with unlimited local code completion and limited monthly cloud AI queries
- **AI Pro and AI Ultimate**: More monthly cloud AI queries, included with some JetBrains subscriptions  
- **AI Enterprise**: Highest usage limits plus enterprise features like user management and custom AI models

You need a valid JetBrains IDE licence and JetBrains Account to use AI features.

## Privacy Settings

JetBrains gives you full privacy controls. Data sharing is opt-in by default.

**Two types of data collection:**
- **Usage data**: Shows which AI features you use. Does not include your source code. Turn off in *Help → Data Sharing*
- **Detailed data**: Includes your questions and AI responses. Not collected unless you explicitly agree

Run in "zero-data-retention" mode by keeping default settings. JetBrains does not permanently store your conversations or code.

## Terms of Use and Privacy Policy

You must agree to JetBrains AI Terms of Service before use. Key points:

- **Data processing**: Your questions and code go to third-party AI providers
- **Ownership**: You keep ownership of your code and data
- **Training**: JetBrains and AI partners do not use your code to train AI models
- **Your responsibility**: Review AI outputs before using them

Data Processing Agreement available for formal compliance documentation.

## Data Management

### Multi-Regional Processing

JetBrains is based in Prague, Czech Republic. Data routes through EU servers but reaches third-party AI providers:

- **OpenAI (GPT)**: United States with zero-data-retention
- **Anthropic (Claude)**: United States with no-retention policy
- **Google (Gemini)**: EU, US, and Asia data centres
- **Amazon Bedrock**: Regional selection available for enterprise users

**Data will often leave the UK and EU.** AI Enterprise plan can address data location concerns.

### Data in Transit

All data uses secure HTTPS connections with modern encryption. Your code is never sent in plain text. Encryption meets typical PSN/GovConnect requirements.

### Data at Rest

By default, JetBrains AI does not store your code or questions on disk. Zero-retention mode stores data only in temporary memory. If detailed data collection is enabled, data is stored for maximum 30 days on EU servers.

## Auditing

Limited audit logging available. No detailed logs of AI queries and responses by default.

**Available:**
- Current session history in IDE (disappears when closed)
- Usage metrics for billing

**Not available:**
- Content logs of "who asked what"
- Built-in audit features for administrators

AI Enterprise plan may offer enhanced logging options.

## Access Controls

Access controlled through JetBrains Accounts and licence entitlements. Only users with active IDE licences can use the service.

**Organisation control:**
- Admin portal for licence assignment
- Single sign-on integration (Enterprise)
- Organisation-wide policies (Enterprise)

**Limitations:**
- Cannot access files you have not opened
- Cannot automatically commit to version control
- Cannot run system commands independently

## Compliance & Regulatory Considerations

**UK GDPR compliance:**
- JetBrains fully complies as EU-based company
- Standard Contractual Clauses for data transfers
- Data Processing Agreements available

**Security standards:**
- ISO 27001-compliant data centres
- Industry-standard security practices
- Regular security reviews

**Key considerations for government:**
1. Data processing outside UK/EU must be acceptable
2. Zero-retention mode should meet data protection requirements
3. Limited audit logging may not meet compliance needs
4. Enterprise plan may be necessary for enhanced control
