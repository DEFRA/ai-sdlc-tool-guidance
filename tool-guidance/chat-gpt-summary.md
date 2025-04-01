# ChatGPT – Summary Report

This is a high-level summary of the [detailed report](chat-gpt-detailed.md)

## 1. Tool Overview

ChatGPT is an AI-driven chatbot available via a web interface at [chatgpt.com](https://chatgpt.com). Developed by OpenAI, it uses advanced language models (such as GPT‑4) to generate conversational responses and assist with tasks like writing, coding, and brainstorming.

The service is offered in several subscription tiers:
- **Free:** Basic access using GPT‑3.5 with standard features.
- **ChatGPT Plus:** A monthly subscription (US$20) that offers enhanced performance and access to GPT‑4.
- **ChatGPT Team:** Designed for small organisations, this plan provides shared workspaces and enhanced user management.
- **ChatGPT Enterprise:** Tailored for large organisations, it offers advanced security, audit logging, custom data retention options, and the ability to store data at rest within Europe.

## 2. Privacy Settings

ChatGPT provides robust privacy controls that enable users to manage their data:
- **Chat History Toggle:** Users can disable chat history via **Settings > Data Controls**. When disabled, conversations are not stored for model training and are retained only for abuse monitoring, then deleted after 30 days. Free and Plus plan users must enable this setting. 
- **Temporary Chat Mode:** Conversations in this mode are treated as ephemeral and are not saved in the persistent sidebar.
- **Data Export and Account Deletion:** Users have the option to export their conversation history or delete their account entirely.
- **Business Plans:** In ChatGPT Team and Enterprise plans, data is automatically excluded from model training by default

## 3. Terms of Use and Privacy Policy

- **User Content Ownership:** Users (or organisations) retain ownership of the content they input and receive, which is essential for intellectual property and confidentiality.
- **Data Review and Retention:** While OpenAI may review or retain data for abuse prevention or legal purposes, clear terms are in place to safeguard user data.
- **Tailored Terms for Business:** Separate business terms and a UK/EEA-specific version are available, ensuring alignment with local legal requirements and the needs of government users.

## 4. Data Management

### 4.1 Multi-Regional Processing

- **Default Storage:** By default, ChatGPT data (including conversation content and account information) is stored on OpenAI's servers in the United States.
- **European Data Residency:** From February 2025, ChatGPT Enterprise and Education customers can opt to have their data stored at rest in Europe. This helps meet European and UK data sovereignty requirements. This option is not available for Free, Plus, or Team plans.

### 4.2 Data in Transit

All communications between the user's browser and the ChatGPT service are encrypted using TLS (Transport Layer Security) version 1.2 or higher.

### 4.3 Data at Rest

All stored user data is encrypted at rest using AES‑256 encryption.

### 4.4 Retention Policies  

  - **Free/Plus:** Data is retained indefinitely when chat history is enabled. When conversations are removed, they are deleted within 30 days. Users can disable chat history, after which their data remains private, is not used for training, and follows the 30-day deletion policy.
  - **Team:** User data remains private, is not used for training, and follows the 30-day deletion policy upon removal.
  - **Enterprise:** Organisations can configure custom data retention periods to meet specific regulatory or internal policies.

## 5. Auditing

- **Audit Logging for Enterprise:** ChatGPT Enterprise offers audit logging via a Compliance API, allowing detailed monitoring of conversation logs and metadata. This supports security oversight and compliance with internal policies.
- **Limited Auditing in Other Plans:** In Team plans, only basic usage metrics are available for administrators, with individual conversation logs remaining private.

## 6. Access Controls

- **Individual Accounts (Free/Plus):** These accounts offer standard security features, including two‑factor authentication.
- **Team Workspaces:** ChatGPT Team provides shared workspaces with administrative tools for user management, though individual chat histories remain private.
- **Enterprise Integration:** ChatGPT Enterprise supports Single Sign-On (SSO), SCIM provisioning, and fine‑grained access controls. This integration allows organisations (including government bodies) to enforce secure access in line with their internal identity management systems.

## 7. Compliance and Regulatory Considerations

ChatGPT adheres to recognised industry standards and regulatory requirements:
- **Security Certifications:** The service holds SOC 2 Type II certification and is listed at CSA STAR Level 1.
- **GDPR and UK Data Protection:** OpenAI supports GDPR compliance through a Data Processing Addendum (DPA) and offers a European data residency option, addressing both EU and UK data protection needs.
- **Additional Standards:** For healthcare or other sensitive sectors, OpenAI is open to signing Business Associate Agreements (BAAs) and undergoes regular third‑party penetration testing and bug bounty programmes.

## 8. References

- [ChatGPT Overview | OpenAI](https://openai.com/chatgpt/overview/#:~:text=Get%20answers,more%20productive)
- [ChatGPT Pricing & Plans | OpenAI](https://openai.com/chatgpt/pricing/#:~:text=Team)
- [Data Controls FAQ | OpenAI Help Centre](https://help.openai.com/en/articles/7730893-data-controls-faq)
- [OpenAI launches data residency in Europe | TechCrunch](https://techcrunch.com/2025/02/06/openai-launches-data-residency-in-europe/)
- [Enterprise privacy at OpenAI | OpenAI](https://openai.com/enterprise-privacy/#:~:text=Who%20owns%20inputs%20and%20outputs%3F)
- [Compliance API for Enterprise Customers | OpenAI Help Centre](https://help.openai.com/en/articles/9261474-compliance-apis-for-enterprise-customers)

