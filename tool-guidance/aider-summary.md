# Aider - Summary

This summary covers the key points from the [detailed guide](aider-detailed.md). Use it to understand how Aider can work in government environments.

## What you need to know

Aider is an AI coding assistant that works in your terminal. It helps government developers write, fix, and improve code using AI models like GPT-4 or Claude.

### What Aider does

- Works with over 100 programming languages
- Connects to your Git version control
- Creates automatic commit messages
- Runs entirely on your computer
- Works with cloud or local AI models
- Lets you chat in plain English to change code

**Important:** Aider is free and open source (Apache 2.0 licence), so you can inspect and modify it.

## Control your privacy

### Your code stays safe

Aider keeps your data secure by default:
- All code stays on your computer
- Never sends your full codebase anywhere
- Only sends specific code snippets when you ask questions
- Runs without internet if you use local AI models

### Turn off data collection

Stop all data sharing:
```bash
aider --analytics-disable
```

Check what would be sent first:
```bash
aider --analytics-log filename.jsonl --no-analytics
```

### Maximum security setup

Use local AI models instead of cloud services to keep everything within your organisation.

## Know your rights

### You own your code

Aider's terms are clear:
- You keep ownership of code you write
- You own code that Aider generates
- Aider cannot use your code without permission

### Data processing

When analytics are on, Aider processes some data:
- No code content goes to Aider's servers
- Only anonymous usage statistics are collected
- All processing happens in the United States

**Review these documents first:**
- Terms & Conditions
- Privacy Policy

## Understand data storage

### What stays on your computer

- All your source code files
- Complete chat conversations
- Git commit history
- Your project files and structure

### What gets shared

Only when you use cloud AI models:
- Specific code snippets you ask about
- Your questions and prompts
- Nothing else leaves your system

### Where data goes

**Analytics (if enabled):** United States servers

**Your code:** Stays on your computer

**AI model data goes to:**
- OpenAI: United States
- Anthropic: United States
- Local models: Your systems only

### Keep data in the UK

For UK data requirements:
- Turn off analytics completely
- Use local AI models only
- Treat as an internal development tool

### Data security

**In transit:** HTTPS/TLS encryption for all connections
**At rest:** Protected by your computer's security
**Your responsibility:** Encrypt your hard drive for sensitive data

## Track what Aider does

### Automatic audit trails

Aider records everything locally:

**Git commits show:**
- Every change Aider makes
- Clear descriptions of what changed
- "(aider)" tag to identify AI changes
- Complete before/after comparisons

**Chat history includes:**
- Your questions and requests
- AI responses and suggestions
- Code snippets discussed
- When everything happened

### Review Aider's work

**See recent changes:**
```bash
git log --oneline --author="aider"
```

**Check a specific change:**
```bash
git show <commit-hash>
```

**Undo the last change:**
```bash
aider /undo
```

**Watch what gets sent to AI:**
```bash
aider --verbose
```

### Control Git operations

**Default behaviour:**
- Saves changes locally only
- Never pushes to remote servers
- You control what gets shared

**Restrict access:**
```bash
aider --no-git              # Stop all Git operations
aider --no-auto-commits     # Make changes but don't save automatically
```

## Control user access

### How Aider runs

Aider uses your computer account permissions:
- Cannot access files you cannot access
- Cannot run commands you cannot run
- Cannot change protected files

### Shell commands

When you use `/run` in chat:
- Only runs commands you type
- Shows all output clearly
- Uses your existing permissions

### Prevent unauthorised use

**System security:**
- Use normal computer security (passwords, locks)
- Control who can install Aider
- Monitor Git for unexpected changes

**Network security:**
- Only connects to AI services you choose
- Can run completely offline
- No hidden connections

## Check compliance needs

### Current certifications

Aider does not have formal security certificates like:
- ISO 27001
- SOC 2
- FedRAMP

This is normal for open source tools that run locally.

### Data protection rules

**GDPR considerations:**
- Analytics processed in United States
- No specific GDPR compliance claims
- Uses consent for data transfers
- Collects minimal personal data

**For UK government:**
- Turn off analytics to avoid US data transfers
- Use local AI models to keep data in UK
- Treat as internal tool, not external service

### Code ownership

You keep full ownership of:
- Original code you write
- Code Aider generates
- All modified versions

Open source licence allows unlimited government use.

## Before you start

### Get approval first

1. **Security review** - Have IT security assess the tool
2. **Legal check** - Verify against department policies
3. **Data classification** - Match AI models to your data sensitivity
4. **Network approval** - Confirm AI service connections are allowed

### Set up securely

1. **Install properly** - Use official sources only
2. **Choose AI models** based on data sensitivity:
   - Local models for sensitive code
   - Cloud models for less sensitive work
3. **Configure privacy:**
   ```bash
   aider --analytics-disable
   ```
4. **Test safely** - Start with non-sensitive code

### Create usage rules

**Good practices:**
- Review all AI-generated code
- Use clear instructions for better results
- Keep chat logs for audits
- Never paste sensitive data in chat
- Use local models for classified work

**Avoid using for:**
- Highly classified code
- Personal data processing
- Production without review
- External repositories

## Get help

**Official support:**
- [Documentation](https://aider.chat/docs/)
- [GitHub](https://github.com/paul-gauthier/aider)
- Email: security@aider.chat

**Training topics:**
- Writing effective prompts
- Reviewing AI code suggestions
- Understanding Git integration
- Security best practices

## Next steps

1. **Start small** - Test on low-risk project
2. **Get feedback** - Ask developers and security team
3. **Update policies** - Refine based on experience
4. **Expand gradually** - Add more projects as confidence grows
5. **Monitor regularly** - Check Git commits and chat logs

**Key choice:** Cloud AI models (faster, more features) or local models (more secure, slower).

Start with local models for sensitive code, cloud models for general development.