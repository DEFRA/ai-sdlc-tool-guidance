# Junie (JetBrains AI Coding Agent)

This summary covers the key points from the [detailed guide](junie-detailed.md). Use it to understand how Junie can work in government environments.

## Tool Overview
Junie is JetBrains’ cloud‑based AI agent for IntelliJ IDEA Ultimate (and other JetBrains IDEs).  
It can analyse a project, generate or refactor code, run tests, and execute terminal commands to fulfil multi‑step development tasks.  
Junie is bundled as a plugin from IDE version 2025.1 and requires an active *JetBrains AI* subscription.  
It relies on large language models (LLMs) hosted by partners such as OpenAI and Anthropic; an offline model is **not yet available** for Junie.  
All changes are shown in‑IDE for developer review – the agent never commits code automatically.

## Privacy Settings
* **Opt-in activation required** – All cloud-assisted AI features, including Junie, are disabled by default. Users must explicitly enable JetBrains AI through the IDE's AI tool widget and accept the JetBrains AI Terms before any code is sent externally. 
* **Data collection controls** – The *data‑sharing* feature is disabled by default. If enabled via Tools | AI Assistant | Data Sharing, it allows JetBrains to collect prompts and responses for product improvement, with a maximum retention period of 30 days.  
* **Selective file exclusion** – Teams can create a `.aiignore` file in their project (similar to `.gitignore`) to prevent sensitive files or folders from being sent to AI models. This provides granular control over what code the AI can access.  
* **Complete user control** – AI plugins, including Junie, can be disabled or completely uninstalled at any time through IDE settings. When disabled, no code or queries are sent from the IDE.

## Terms of Use and Privacy Policy
* **JetBrains AI Terms of Service** – code and prompts are forwarded to third‑party LLM providers solely to generate a response; they are **not used to train any model**.  
* **JetBrains Privacy Notice** – JetBrains s.r.o. (Czech Republic) is the data controller and follows GDPR / UK GDPR.  
* Data Processing Agreement (DPA) and sub‑processor list are available for organisational due‑diligence.  
* Users remain responsible for the legality of any content they submit.

## Data Management

### Multi‑Regional Processing
JetBrains AI runs on AWS and Google Cloud infrastructure located in the **EU, US and Asia**.  
Therefore data may leave the UK. *JetBrains AI Enterprise* offers regional or on‑premises hosting, but **Junie is not yet supported** under that plan.

### Data in Transit
All traffic between the IDE, JetBrains and the LLM provider is encrypted with **TLS 1.2+**.  
Contractual clauses require providers to keep data confidential and discard it after processing.

### Data at Rest
* **Zero‑retention by default** – code and prompts are discarded once a reply is returned.  
* If *data‑sharing* is enabled, prompts and responses are stored (encrypted) for up to **30 days**.  
* Optional semantic‑search indexing stores vector embeddings (not raw code) for active projects.  
* All data at rest is encrypted by the underlying cloud platform.

## Auditing
Junie shows a live activity log in its tool window, and all edits appear in the IDE’s *diff/undo* history.  
There is **no central audit log** today; organisations must rely on version‑control reviews.  
JetBrains has signalled that enterprise audit features are on the roadmap.

## Access Controls
* Access is tied to the developer’s **JetBrains Account** and AI licence; admins can revoke usage centrally.  
* The agent runs with the **same OS and repository rights as the developer** – no elevated privileges.  
* `.aiignore` and project‑level settings limit what the agent can read.  
* Junie cannot push commits; humans remain in control of repository operations.

## Compliance & Regulatory Considerations
* **GDPR / UK GDPR compliant** – EU‑based data controller, user‑controlled data sharing, subject‑access rights.  
* **SOC 2 Type II** audited for security, availability and confidentiality.  
* No public ISO 27001 certificate (as of July 2025).  
* Cloud processing outside the UK may be unsuitable for *OFFICIAL‑SENSITIVE* workloads; on‑prem support is awaited.  
* JetBrains contracts forbid model providers from training on customer data, reducing IP‑leakage risk.

## References
1. JetBrains Help – “Junie” overview: <https://www.jetbrains.com/help/idea/junie.html>  
2. JetBrains Docs – “Getting started with Junie”: <https://www.jetbrains.com/help/idea/junie-getting-started.html>  
3. JetBrains AI FAQ: <https://www.jetbrains.com/help/idea/ai-assistant-faq.html>  
4. JetBrains AI Terms of Service: <https://www.jetbrains.com/legal/docs/terms/ai_tos.html>  
5. JetBrains Privacy Notice: <https://www.jetbrains.com/legal/docs/privacy/privacy.html>  
6. JetBrains Data Collection & Use Policy: <https://www.jetbrains.com/help/idea/ai-data-collection.html>  
7. JetBrains AI Privacy & Security Q&A: <https://www.jetbrains.com/help/idea/ai-privacy-security.html>  
8. DevClass, 16 Apr 2025 – “JetBrains goes live with Junie AI agent”: <https://devclass.com/2025/04/16/jetbrains-goes-live-with-junie-ai>  
9. JetBrains Trust Centre: <https://www.jetbrains.com/company/trust>
