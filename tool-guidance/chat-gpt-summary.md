# ChatGPT – Summary

**Approval status:** Approved with restrictions - you may use this tool, but be cautious about what data you share. You must not enter or share anything that is not already published in the public domain.

This summary covers the key points from the [detailed guide](chat-gpt-detailed.md). Use it to understand how ChatGPT can work in government environments.

## What ChatGPT does

ChatGPT is an AI chatbot you can access at [chatgpt.com](https://chatgpt.com). OpenAI built it using large language models to create conversational responses and help with writing, coding, and brainstorming tasks.

The service has different subscription levels:
- **Free:** Basic access using smaller GPT models with standard features
- **ChatGPT Plus:** Monthly subscription (US$20) with enhanced performance and GPT advanced model access
- **ChatGPT Team:** For small organisations with shared workspaces and user management
- **ChatGPT Enterprise:** For large organisations with advanced security, audit logging, custom data retention, and European data storage options

## Privacy controls

ChatGPT gives you strong privacy controls:
- **Chat history toggle:** Turn off chat history in **Settings > Data Controls**. When off, conversations are not stored for model training and are kept only for abuse monitoring, then deleted after 30 days. Free and Plus users must enable this setting manually.
- **Temporary chat mode:** Conversations in this mode are temporary and do not appear in your persistent chat history
- **Data export and account deletion:** Export your conversation history or delete your account completely
- **Business plans:** ChatGPT Team and Enterprise exclude data from model training by default

## Terms and data ownership

Key legal points:
- **You own your content:** Users (or organisations) keep ownership of content they input and receive
- **Data review and retention:** OpenAI may review or keep data to prevent abuse or for legal reasons, but clear terms protect your data
- **Business terms:** Separate business terms and UK/EEA versions align with local legal requirements for government users

## Where your data goes

### Data storage locations

- **Default storage:** ChatGPT stores data (including conversation content and account information) on OpenAI servers in the United States by default
- **European data residency:** From February 2025, ChatGPT Enterprise and Education customers can choose to store their data at rest in Europe. This helps meet European and UK data sovereignty requirements. This option is not available for Free, Plus, or Team plans.

### Data protection in transit

All communications between your browser and ChatGPT use TLS (Transport Layer Security) version 1.2 or higher encryption.

### Data protection at rest

All stored user data uses AES‑256 encryption at rest.

### How long data is kept

- **Free/Plus:** Data is kept indefinitely when chat history is enabled. When you remove conversations, they are deleted within 30 days. You can turn off chat history - then your data stays private, is not used for training, and follows the 30-day deletion policy.
- **Team:** User data stays private, is not used for training, and follows the 30-day deletion policy when removed.
- **Enterprise:** Organisations can set custom data retention periods to meet specific regulatory or internal policies.

## Audit logs

- **Enterprise audit logging:** ChatGPT Enterprise offers audit logging through a Compliance API, allowing detailed monitoring of conversation logs and metadata. This supports security oversight and compliance with internal policies.
- **Limited auditing in other plans:** Team plans only have basic usage metrics for administrators - individual conversation logs stay private.

## Access controls

- **Individual accounts (Free/Plus):** Standard security features including two‑factor authentication
- **Team workspaces:** Shared workspaces with administrative tools for user management, though individual chat histories stay private
- **Enterprise integration:** Single Sign-On (SSO), SCIM provisioning, and detailed access controls. This integration lets organisations (including government bodies) enforce secure access using their internal identity management systems.

## Compliance and regulation

ChatGPT meets recognised industry standards and regulatory requirements:
- **Security certifications:** SOC 2 Type II certification and CSA STAR Level 1 listing
- **GDPR and UK data protection:** OpenAI supports GDPR compliance through a Data Processing Agreement (DPA) and offers European data residency, addressing both EU and UK data protection needs
- **Additional standards:** For healthcare or other sensitive sectors, OpenAI can sign Business Associate Agreements (BAAs) and undergoes regular third‑party penetration testing and bug bounty programmes
