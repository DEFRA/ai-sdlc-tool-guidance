# Google Gemini - Summary

This summary covers the key points from the [detailed guide](google-gemini-detailed.md). Use it to understand how Google Gemini can work in government environments.

## What you need to know

Google Gemini is an AI chat assistant that helps government staff write content, answer questions, and analyse information. You access it through a web browser or mobile app.

### What Gemini does

- Answers questions and explains topics
- Writes and edits documents
- Summarises and analyses content
- Creates images and presentations
- Works with Gmail, Google Drive, and other Google apps
- Offers voice conversations ("Gemini Live")

### How to access it

- Sign in with a Google Account at `gemini.google.com`
- Use the mobile app
- Access through Google Workspace (enterprise version)

### Choose the right version

**Free version:** Personal use only - not suitable for government work

**Enterprise version:** For organisations through Google Workspace - use this for all government work

## Control your privacy

### Free version risks

**Default settings:**
- Saves chat history for 18 months
- Uses your conversations to improve Google's AI
- Human reviewers may read your chats

**Why government should avoid:** Your conversations may be seen by Google staff and used to train their AI systems.

### Enterprise version protections

**Better security:**
- Your chats are not used to train AI
- No human reviewers read conversations
- Data stays in your organisation's Google Workspace
- Same security as Gmail and Google Drive

**Administrator controls:**
- IT teams control who can use Gemini
- Data follows your organisation's policies
- Retention settings can be configured

### Protect sensitive information

**Never enter:**
- Classified or confidential data
- Personal information about citizens
- Security passwords or credentials
- Commercially sensitive information

**Remember:** Even enterprise data may be processed outside the UK during AI conversations.

## Know your legal position

### Free version terms

Using a personal Google Account means:
- Google's standard terms apply
- Google Ireland provides the service in Europe
- Your conversations may improve Google's services
- You must follow Google's AI usage rules

### Enterprise version terms

Using Google Workspace means:
- Your organisation's Google agreement applies
- Google processes data on your behalf (you stay in control)
- Your conversations are not used to train AI
- GDPR protections apply through existing agreements

**Key documents to review:**
- Google Terms of Service
- Gemini Apps Privacy Notice
- Google Workspace Terms
- AI Prohibited Use Policy

## Understand data handling

### Where your data goes

**Important:** Google processes data in data centres worldwide - it cannot guarantee your data stays in the UK or EU during AI processing.

**What this means:**
- Data may leave UK jurisdiction during conversations
- Processing happens where Google has capacity
- Encryption and legal protections apply to transfers
- Saved documents can be stored in your chosen region

### Data security

**In transit:** All communications use HTTPS/TLS encryption

**At rest:** All content is encrypted on Google's servers

**Limitation:** Client-side encryption does not work with Gemini

### How long data is kept

**Free version:**
- Chat history: 18 months (you can change to 3-36 months)
- Deleted chats: Removed immediately
- Training data: Up to 3 years if used for AI improvement

**Enterprise version:**
- Chat history: 18 months default
- Custom retention: Coming soon for administrators
- Training use: Never happens

**All versions:** Google keeps recent chats for 72 hours for service quality

## Track usage

### What gets logged

**Currently available:**
- When Gemini accesses your Google Drive files
- Which user triggered the action
- Time and date of file access
- Which files were involved

**Not logged:**
- Your actual questions
- Gemini's responses
- General chat without file access

### Access logs

**For administrators:**
1. Go to Google Workspace Admin Console
2. Use Investigation tool
3. Look for "Gemini content access" events
4. Export via Workspace Audit API

**Future improvements:** Google plans to log more activities including Gmail integration and other app interactions.

## Control access

### User authentication

**How users get in:**
- Sign in with Google Account
- Enterprise users need Google Workspace accounts
- Same security features apply (two-factor authentication, etc.)

### Administrator controls

**For enterprise users:**
- Turn Gemini on or off for specific users
- Control which licences include Gemini
- Set age restrictions (18+ only)
- Manage connections to other Google services

**Workspace Extensions:**
- Allow or block Gemini's access to Gmail, Drive, etc.
- Users can control their own permissions
- Administrators can disable all extensions

### User permissions

**Inside Gemini:**
- All users have the same capabilities
- No different roles once signed in
- Access control happens at login

**File access:**
- Users must give permission for Gemini to read files
- Permissions can be changed anytime
- Administrators can override user settings

## Check compliance

### Security certifications

Gemini has these formal certifications:
- **ISO 27001** - Information security management
- **ISO 27701** - Privacy management
- **ISO 27017/27018** - Cloud security and privacy
- **ISO 42001** - AI management (first chat AI to get this)
- **SOC 1, 2, 3** - Service controls
- **FedRAMP High** - US government security standard

### Data protection

**GDPR compliance:**
- Data Processing Agreement for enterprise users
- Google acts as processor, you control data
- User rights supported (access, delete, object)
- Impact assessment resources available

**Other compliance:**
- **HIPAA** - Healthcare data protection
- **COPPA/FERPA** - Education privacy
- **EU AI Act** - Preparing for new regulations

### UK government considerations

**Strengths:**
- Strong international security certificates
- GDPR compliance mechanisms
- Enterprise security controls
- Clear data handling documentation

**Things to consider:**
- No guarantee data stays in UK during processing
- No UK-specific government certificates yet
- May need Data Protection Impact Assessment
- Not in UK procurement frameworks yet

## Before you start

### Get approval first

1. **IT security review** - Have security team assess the service
2. **Legal review** - Check against your data policies
3. **Data classification** - Match use to data sensitivity
4. **Privacy assessment** - Complete DPIA if handling personal data

### Choose correctly

**Use enterprise version for:**
- Any government work
- Official documents
- Work-related content
- When you need audit trails

**Never use free version for:**
- Government business
- Official information
- Personal data processing
- Confidential content

### Set up safely

**For administrators:**
1. Configure access through Google Workspace Admin
2. Set retention policies when available
3. Enable audit logging
4. Control app integrations
5. Train users on proper use

**For users:**
1. Use your official Google Workspace account
2. Understand what Gemini can access
3. Set file permissions carefully
4. Never input sensitive information

## Get help

**Official resources:**
- [Gemini Privacy Hub](https://support.google.com/gemini/answer/13594961)
- [Google Workspace Help](https://support.google.com/a/answer/13822685)
- [Privacy Notice](https://support.google.com/gemini/answer/13594961)

**UK government guidance:**
- [Data Protection Act 2018](https://gov.uk/data-protection)
- [NCSC Cloud Security](https://ncsc.gov.uk/collection/cloud-security)
- [GOV.UK AI Guidance](https://gov.uk/guidance/artificial-intelligence)

**Training topics:**
- Understanding AI limitations
- When not to use AI
- Data protection rules
- Writing effective prompts
- Reviewing AI outputs

## Next steps

1. **Start with pilot** - Test with small group using non-sensitive content
2. **Gather feedback** - Get user and security team input
3. **Review logs** - Monitor usage and access patterns
4. **Update policies** - Improve guidelines based on experience
5. **Expand carefully** - Scale with proper controls

**Key rule:** Only use enterprise version for government work to get proper data protection and compliance.

**Remember:** AI assists human decisions - it does not replace them. Always review AI content before using officially.