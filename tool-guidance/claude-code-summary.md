# Claude Code - Summary

**Approval status:** Under review - this tool is not currently approved for use. We are reviewing it for potential approval, but cannot commit to if or when this might happen.

This summary covers the key points from the [detailed guide](claude-code-detailed.md). Use it to understand how Claude Code can work in government environments.

## What you need to know

Claude Code is an AI coding assistant that works in your terminal. It helps users write, fix, and test code while keeping your data secure.

### What Claude Code does

- Reads and understands large codebases
- Writes and fixes code for you  
- Runs tests and commands
- Creates pull requests
- Works with VS Code and Git

**Important:** You stay in control. Claude Code asks permission before changing files or running commands.

### How it protects your code

Claude Code runs on your computer, not in the cloud. It only sends specific questions and code snippets for analysis - never your entire codebase.

## Set up privacy controls

### Basic privacy

Claude Code automatically:
- Keeps your full codebase on your computer
- Only sends code you ask about
- Asks before making any changes

### Government privacy settings

If your department uses Claude Enterprise, administrators can:
- Stop feedback being sent to Anthropic
- Turn off all usage tracking
- Disable error reports

**Turn off data sharing completely:**
```
CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
```

## Understand data storage

### Where your data goes

**Default location:** United States servers

**UK and EU options available:**

**Keep data in the UK:**
- Use AWS Bedrock with UK regions
- Meets government security standards

**Keep data in the EU:**
- Use Google Cloud with London or Frankfurt regions
- Data stays within EU borders

**Action:** Contact Anthropic to set up UK or EU hosting if required.

### How long data is kept

**Standard:** Up to 30 days maximum

**Enterprise options:**
- 7 days or shorter
- Zero retention (deleted immediately)

**Exception:** Policy violations may be kept for 2 years for investigation.

### Data security

**In transit:** All data encrypted with TLS (bank-level security)
**At rest:** AES-256 encryption (industry standard)

**Your responsibility:** Encrypt your computer's hard drive for sensitive data.

## Monitor usage

### What gets tracked

Enterprise audit logs show:
- Who logged in and when
- When conversations started  
- When files were uploaded
- All user actions with timestamps

**Important:** Logs do not contain your actual code or conversations.

### Access your logs

Administrators can:
- Export logs from Anthropic Console
- Download 6 months of activity data
- Connect to security monitoring tools (SIEM)

### Real-time monitoring

Connect Claude Code to your existing monitoring:
- Splunk
- CloudWatch
- Other OpenTelemetry tools

## Control user access

### Connect to your login system

Link Claude Code to:
- Azure Active Directory
- Google Workspace
- Any SAML or OAuth system

This ensures staff use official credentials and two-factor authentication.

### Set user permissions

**Choose the right role for each person:**
- **Primary Owner:** Full control over settings
- **Admin:** Can change settings and export data
- **Developer:** Can use Claude Code
- **Member:** Basic chat only

**Prevent unauthorised access:** Restrict to your organisation's email domain.

### Automate user management

Use SCIM to:
- Create accounts for new staff automatically
- Remove access when people leave
- Keep accounts in sync with HR systems

## Check compliance requirements

### Security certifications

Anthropic has:
- **ISO 27001** (information security)
- **ISO 42001** (AI risk management) 
- **SOC 2 Type II** (operational security)

### Data protection

- GDPR compliant
- HIPAA eligible (high privacy standards)
- Uses Irish company for EU customers

### Government approval

**FedRAMP High** approved (US government standard) - shows it meets high security requirements.
