# Aider - Detailed Guide

## What Aider does

Aider is an AI coding assistant that works in your terminal. It helps developers write, edit, and fix code by connecting to AI models like GPT-4 or Claude.

**Key features:**
- Works with over 100 programming languages
- Integrates with Git version control
- Creates automatic commit messages
- Runs entirely on your computer
- Supports both cloud and local AI models

**How it works:** You chat with Aider in plain English, asking it to make code changes. It understands your project context and applies changes directly to your files.

**Open source:** Aider is free and open source (Apache 2.0 licence), so you can inspect and modify the code.

## How your data stays private

### Your code stays local

Aider runs on your computer and does not send your code to Aider's servers. It only sends specific code snippets to the AI model you choose (like OpenAI or Anthropic) when you ask questions.

**What Aider never collects:**
- Your source code
- Chat conversations
- API keys
- Personal information

### Analytics are optional

Aider may collect anonymous usage statistics, but only if you agree. These include:
- Which AI models you use
- How often you use certain features
- Error messages (without code content)

**Turn off analytics completely:**
```bash
aider --analytics-disable
```

**Check what would be sent:**
```bash
aider --analytics-log filename.jsonl --no-analytics
```

### Use local AI models

For maximum privacy, use Aider with local AI models instead of cloud services. This keeps all your code and conversations on your systems.

## Legal terms and data ownership

### You own your code

Aider's terms are clear:
- You keep ownership of all code you write
- You own any code Aider generates
- Aider cannot use your code to improve their service without permission

### Data processing

Aider acts as a data processor when you use their analytics service. However:
- No code content is processed by Aider
- Only anonymous usage metrics are collected
- Data is processed in the United States

**Important:** Review these documents before using Aider:
- Terms & Conditions
- Privacy Policy

## Data storage and security

### Where your data goes

**Default location:** United States servers (for analytics only)

**Your code:** Stays on your computer and is never sent to Aider's servers

**AI model data:** Goes to whichever AI service you choose:
- OpenAI (United States)
- Anthropic (United States)
- Local models (your infrastructure)

### Data retention

**Aider's servers:** No specific retention policy stated - assume analytics data is kept indefinitely

**Your computer:** 
- Chat history saved in `.aider.chat.history.md`
- All changes saved in Git commits
- You control how long to keep these files

**AI model providers:** Each has their own retention policy:
- OpenAI: 30 days for abuse monitoring
- Anthropic: 30 days maximum (configurable)

### Data security

**In transit:** All connections use HTTPS/TLS encryption

**At rest:** 
- Aider uses standard cloud security practices
- Your local files are protected by your computer's security
- Ensure your hard drive is encrypted for sensitive data

## Tracking and audit logs

### What gets recorded locally

Aider creates comprehensive audit trails on your computer:

**Git commits:** Every change Aider makes is automatically committed to Git with:
- Clear commit messages describing what changed
- "(aider)" tag in the author name
- Complete diff showing exactly what was modified

**Chat transcripts:** Full conversation history saved in `.aider.chat.history.md` including:
- Your questions and requests
- AI responses
- Code snippets discussed
- Timestamps for all interactions

### How to review Aider's actions

**Check recent changes:**
```bash
git log --oneline --author="aider"
```

**Review a specific change:**
```bash
git show <commit-hash>
```

**Undo the last change:**
```bash
aider /undo
```

**Read chat history:**
```bash
cat .aider.chat.history.md
```

### Monitoring options

**Verbose mode:** See exactly what Aider sends to AI models:
```bash
aider --verbose
```

**Disable Git integration:** Prevent automatic commits:
```bash
aider --no-auto-commits
```

**Block all Git operations:**
```bash
aider --no-git
```

## User access and permissions

### How Aider runs

Aider runs under your user account with the same permissions you have:
- Cannot access files you cannot access
- Cannot run commands you cannot run
- Cannot write to protected directories

### Controlling Git operations

**Default behaviour:**
- Commits changes locally
- Never pushes to remote repositories
- Requires your explicit command to push

**Restrict Git access:**
```bash
aider --no-git                    # Disable all Git operations
aider --no-auto-commits          # Make changes but don't commit
aider --git-commit-verify        # Enable Git commit hooks
```

### Shell command execution

Aider can run shell commands when you use `/run` in the chat:
- Only runs commands you explicitly request
- Uses your system permissions
- Displays output in the chat

**Example:**
```
You: /run pytest tests/
Aider: Running: pytest tests/
[test output appears here]
```

### Preventing unauthorised actions

**System security:**
- Use standard workstation security (passwords, screen locks)
- Control who can install and run Aider
- Monitor Git repositories for unexpected commits

**Network security:**
- Aider only connects to AI services you configure
- Does not phone home for authentication
- Can run completely offline with local models

## Compliance and regulations

### Current certifications

Aider does not hold formal security certifications like:
- ISO 27001
- SOC 2
- FedRAMP

This is typical for open source tools that focus on local operation rather than cloud services.

### Data protection compliance

**GDPR considerations:**
- Analytics data is processed in the United States
- No explicit GDPR compliance statements
- Relies on user consent for data transfers
- Minimal personal data collection

**For UK government use:**
- Turn off analytics to avoid international data transfers
- Use local AI models to keep all data within UK jurisdiction
- Treat as an internal development tool rather than external service

### Intellectual property

**Code ownership:** You retain full ownership of:
- Original code you write
- Code that Aider generates
- Modified versions of your code

**Open source licence:** Apache 2.0 allows government use with no restrictions

## Before you start using Aider

### Get approval first

1. **Security review:** Have your IT security team assess the tool
2. **Legal review:** Check terms against your department's policies
3. **Data classification:** Ensure your code is suitable for the AI models you plan to use
4. **Network policy:** Confirm connections to AI services are allowed

### Set it up securely

1. **Install from official sources:** Use pip or conda to install Aider
2. **Choose your AI model:** Select based on your data classification:
   - Local models for sensitive code
   - Cloud models for less sensitive work
3. **Configure privacy settings:**
   ```bash
   aider --analytics-disable    # Turn off analytics permanently
   ```
4. **Set up Git properly:** Ensure commits are signed if required
5. **Test with non-sensitive code first**

### Create usage guidelines

**Recommended practices:**
- Review all AI-generated code before committing
- Use descriptive prompts to get better results
- Keep chat logs for audit purposes
- Don't paste sensitive data into chat
- Use local models for classified projects

**Restrict usage for:**
- Highly classified code
- Code containing personal data
- Production systems without review
- External repositories

## Getting help and support

### Community support

**Official resources:**
- [Aider documentation](https://aider.chat/docs/)
- [GitHub repository](https://github.com/paul-gauthier/aider)
- [Discord community](https://discord.gg/Tv2uQnR)

### Reporting issues

**For bugs or feature requests:**
- Use GitHub issues (public)
- Check existing issues first
- Provide minimal examples

**For security issues:**
- Contact: security@aider.chat
- Do not post sensitive information publicly

### Training your team

**Key topics to cover:**
- How to write effective prompts
- Reviewing AI-generated code
- Understanding Git integration
- Security best practices
- When not to use AI assistance

## Next steps

1. **Start with a pilot:** Test Aider on a small, non-sensitive project
2. **Gather feedback:** Get input from developers and security team
3. **Refine guidelines:** Update usage policies based on experience
4. **Scale gradually:** Expand to more projects as confidence grows
5. **Monitor usage:** Regular review of Git commits and chat logs

**Key decision:** Choose between cloud AI models (faster, more capable) or local models (more secure, slower).

For most government use cases, start with local models for sensitive code and cloud models for less sensitive development work.