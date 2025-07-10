# Google NotebookLM

This summary covers the key points from the [detailed guide](notebooklm-detailed.md). Use it to understand how Google NotebookLM can work in government environments.

## Tool Overview

Google NotebookLM is an AI‑powered note‑taking and research tool that helps users organise, query and summarise their own source documents.  
It runs on Google’s cloud platform and is available in two versions:

* **Personal NotebookLM** – free for anyone with a personal Google account.  
* **NotebookLM for Google Workspace** – an enterprise variant that sits inside an organisation’s existing Workspace tenant and offers extra security, audit and admin controls.

Users create *notebooks*, attach documents (for example PDFs, Docs or web pages) and then ask questions in plain language. NotebookLM answers using only the attached sources and cites every excerpt it relies on. The service is currently in public preview and supports more than 35 languages for input and output.

## Privacy Settings

* NotebookLM does **not** use customer content to train Google’s foundation models.  
* In the Workspace edition, data stays inside the organisation’s Google tenant. Public sharing is disabled by default.  
* Personal users can choose whether Google Support may review their content if they raise a ticket.  
* Users can delete notebooks at any time; admins can set retention rules centrally.

## Terms of Use and Privacy Policy

* **Personal accounts** – covered by the standard Google Terms of Service and Privacy Policy.  
* **Workspace accounts** – covered by the Google Workspace Agreement and Data Processing Amendment, which meet UK GDPR requirements.  
* Both variants commit that NotebookLM content is processed only to provide the service and is never used for advertising.

## Data Management

### Multi-Regional Processing

NotebookLM runs in Google’s global data‑centre network.  
Workspace admins can pin data to the UK, EU or US if required; enterprise customers can also restrict access using Virtual Private Cloud Service Controls. Personal accounts currently default to the US.

### Data in Transit

All traffic between the user, the application tier and storage back‑end is encrypted with TLS 1.2 +. Workspace customers may enforce private access over BeyondCorp Enterprise or a trusted VPN.

### Data at Rest

Content is encrypted with AES‑256 using Google‑managed keys. Workspace Enterprise customers can supply Customer‑Managed Encryption Keys (CMEK). Back‑ups are held for up to 30 days.

## Auditing

Workspace and Enterprise versions write detailed audit events to Cloud Logging: notebook created, file added, sharing changed and so on.  
Google also provides *Access Transparency* logs that show any Google staff access, subject to customer approval.

## Access Controls

* **Authentication** – Google Identity or SSO via SAML/OIDC.  
* **Authorisation** – notebook‑level sharing, inherited from Google Drive permissions.  
* **Admin guardrails** – turn the service on/off for groups, block external sharing, apply Data Loss Prevention and Context‑Aware Access.  
* **Network controls** – VPC Service Controls and BeyondCorp rules can fence traffic to trusted devices and locations.

## Compliance & Regulatory Considerations

Google relies on its existing certifications for the underlying cloud and Workspace platform, including:

* ISO 27001, 27017, 27018  
* SOC 2 Type II  
* UK GDPR / DPA 2018 (processor commitments)  
* FedRAMP Moderate (Workspace scope)  
* HIPAA and PCI DSS (supported where applicable)

NotebookLM itself is not yet PSN‑assured, but the inherited controls meet the Cabinet Office *OFFICIAL* security classification when combined with local policies.

## References

* Google NotebookLM Help Centre – *Privacy and security*  
* Google Workspace Security Whitepaper  
* Google Cloud Compliance Resource Centre  
* Google Trust & Safety: Encryption in Transit and at Rest
