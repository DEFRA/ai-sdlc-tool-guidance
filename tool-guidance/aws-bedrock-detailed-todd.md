# AWS Bedrock

## 1. Tool Overview

**Amazon Bedrock** is a fully managed **generative AI service** on AWS that provides access to a choice of **high-performing foundation models (FMs)** from leading AI companies via a single API. It allows developers to build and scale AI applications without managing infrastructure. Bedrock supports **text, image, and multimodal FMs** from various providers, including **Amazon’s own Titan/Nova models, Anthropic’s Claude family, AI21 Labs, Cohere, Meta’s Llama 2/3, Mistral AI, and Stability AI’s text-to-image models**. The **primary website** for Amazon Bedrock is the **AWS Bedrock product page** on the AWS website (accessible via the AWS console and documentation).

Key capabilities of Bedrock include:

- **Foundation Model Access:** One API to access large language models (LLMs) and generative AI models for tasks like text generation, summarization, Q&A, translation, and image generation.
    
- **Customization:** Fine-tuning base models with proprietary data (via tagging or continued pre-training) to create private, exclusive model variants.
    
- **Integrated Tools:** Features such as prompt management, retrieval augmented generation (RAG), and **Bedrock Agents** – managed agents that connect to APIs and knowledge bases to perform complex tasks.
    
- **Serverless Deployment:** Fully managed, **serverless experience** for deploying and scaling models securely within AWS environments.
    

## 2. Privacy Settings

**Amazon Bedrock is designed with privacy in mind**. Customers maintain control over their content and **Bedrock does not store or use prompts or outputs to improve models**. Key privacy features and configurations include:

- **No Retention of Inputs/Outputs:** By default, **prompts and completions are not logged or retained by Bedrock**, and AWS does not use them to train underlying models or share them with third parties.
    
- **Private Model Customization:** When you fine-tune a model on Bedrock, it uses a **private copy of the base model**, ensuring that **your training data and the customized model remain private to your account**. Model providers (e.g., Anthropic, Cohere) **cannot access your fine-tuned model or data**.
    
- **VPC and PrivateLink Integration:** Customers can **keep data traffic off the public internet** by using **AWS PrivateLink** to directly connect their Amazon VPC to Bedrock’s API endpoints. This configuration ensures data stays within the AWS network and region.
    
- **Encryption Controls:** Bedrock encrypts data in transit and at rest by default, and customers can manage their own keys via **AWS Key Management Service (KMS)** (detailed in Section 4.2 and 4.3). You can configure **KMS encryption for model artifacts, agents, and other resources** in Bedrock for additional privacy control.
    
- **Content Filtering & Guardrails:** Bedrock implements **automated content moderation** (abuse detection) to filter sensitive or harmful content, aligning with AWS’s Acceptable Use Policy. Additionally, Bedrock offers **configurable guardrails** (e.g., deny lists for certain terms or topics) to help customers prevent the generation of unwanted or sensitive content.
    

**AWS Documentation on Privacy:** The AWS Bedrock **security and privacy page** (linked from AWS Bedrock Resources) provides further details on how data is handled. For example, AWS clarifies that **personal data inadvertently present in training datasets is handled under AWS’s legitimate interests** and **not specifically used to identify individuals**. AWS’s **Data Privacy FAQ** and **Global Data Processing Addendum (DPA)** also apply to Bedrock usage, ensuring GDPR-aligned protections for personal data.

## 3. Terms of Use and Privacy Policy

For AWS Bedrock, the key terms and policies include:

- **AWS Service Terms:** Bedrock usage is governed by the **AWS Service Terms** (see Section 50.12 specific to Amazon Bedrock). This section notes that _third-party models_ on Bedrock are treated as **“Third-Party Content”**, subject to their own license terms (e.g., model-specific EULAs) in addition to AWS terms. It also allows AWS to share **non-content usage information** with third-party model providers for usage tracking. Noteworthy Bedrock-specific terms:
    
    - **Automated Abuse Detection:** AWS may employ automated tools to detect misuse (e.g., illicit content, policy violations) and **share details with model providers if required**.
        
    - **Fine-Tuned Models:** If you customize a model, you have exclusive use of that model. **Third-party providers have no access to your fine-tuned model**, and AWS will not use it except as needed to provide the service or if legally compelled.
        
    - **Acceptable Use:** All usage must comply with AWS’s **Acceptable Use Policy**, meaning UK Government users should avoid inputting unlawful or highly sensitive content that violates these terms (e.g., no use for hate speech, illicit behavior, etc.).
        
- **Bedrock Model EULAs:** Each third-party model (Anthropic Claude, AI21 Jurassic, etc.) has an **End User License Agreement (EULA)** accessible via the Bedrock console. These EULAs outline **permitted use cases and restrictions** (for instance, some models may restrict use in certain domains or require usage reporting).
    
- **AWS Customer Agreement or Enterprise Agreement:** Government customers typically operate under the standard **AWS Customer Agreement** (or a customised public sector agreement). This sets the overall terms for using AWS services, including compliance with law, data security responsibilities, and liability clauses.
    
- **AWS Privacy Notice:** AWS’s general **Privacy Notice** (updated **21 February 2025**) explains how AWS collects and processes personal information in AWS services ([AWS Privacy](https://aws.amazon.com/privacy/#:~:text=Privacy%20Notice)). Importantly, it states that **customer content (data you upload to AWS)** is not covered by the public Privacy Notice, because AWS _does not access or use customer content except to provide the services and as legally required_. Instead, handling of customer content is addressed by the contract and the **AWS Data Privacy FAQ**. In essence, **the customer (UK government agency) retains ownership and control of all data input into Bedrock**, and AWS commits to strong confidentiality of that content.
    
- **Data Processing Addendum (DPA):** AWS offers a **GDPR-compliant DPA** (including the UK GDPR and EU SCCs) that automatically applies whenever AWS processes personal data on behalf of customers. This means that for any personal data in prompts or training data, AWS acts as a data processor under GDPR, and the **Global AWS DPA** governs this processing with commitments to confidentiality, security, and EU/UK safeguards.
    
- **Links to Terms & Policies:**
    
    - _AWS Service Terms (Section 50.12 for Bedrock)_ – **AWS Service Terms**.
        
    - _AWS Privacy Notice_ – **AWS Privacy Notice** ([AWS Privacy](https://aws.amazon.com/privacy/#:~:text=Privacy%20Notice)).
        
    - _AWS Data Privacy FAQ_ – **AWS Data Privacy FAQ** (accessible via AWS’s Compliance or Privacy Center).
        
    - _Model Provider EULAs_ – Accessible in the **Bedrock Console** under “Model Access”.
        
    - _Acceptable Use Policy_ – **AWS Acceptable Use Policy** (applicable to all AWS services).
        

For public sector use, it’s crucial to review these terms for any restrictions on **sensitive data categories**, onward transfer, or law enforcement access. Notably, AWS has stated no _additional_ terms specific to UK Government beyond standard AWS agreements, but agencies should confirm if a **G-Cloud or OJEU specific contract** is in place.

## 4. Data Management

### 4.1 Server Location and Data Residency

Amazon Bedrock is available in multiple AWS Regions worldwide, including regions in the **UK and EU**. Notable points about data residency:

- **Regional Control:** When using Bedrock, you **choose the AWS Region** where to invoke the service (e.g., London `eu-west-2`, or other EU regions) and **content is stored and processed in that region** by default. AWS will not move or replicate your content outside the regions you select **without your agreement**. This aligns with data residency needs of UK government projects, as agencies can confine activities to UK or approved regions (e.g. **London, Ireland, Frankfurt**).
    
- **Regions Supported:** As of early 2025, Bedrock’s foundation models are hosted in regions such as **EU-West-2 (London)** and **EU-West-1 (Ireland)**, among others. UK customers can opt for the London region for lowest latency and local compliance. Bedrock endpoints exist in **eu-west-2 (London)** as listed in AWS endpoints documentation.
    
- **GovCloud and Cross-Region:** For highly sensitive data, **AWS GovCloud (US)** supports Bedrock with FedRAMP High authorization. However, that is a US sovereign cloud. In the UK context, **no separate GovCloud UK** exists; instead, standard regions with certifications (ISO, etc.) are used. **Cross-region inference**: Some Bedrock features (like certain latency-optimized inference) might perform cross-region calls (e.g., to us-east-2 in preview). UK users handling OFFICIAL-SENSITIVE data should disable or avoid any feature that routes requests outside approved regions. By default, if you call Bedrock in London, the data stays in London’s AWS network.
    
- **Data Sovereignty Controls:** AWS provides tools like **AWS Control Tower and AWS Artifact** to ensure governance of region usage. While **Bedrock itself does not offer a “UK only” toggle**, UK agencies can enforce usage of EU/UK regions through IAM policies and endpoint configuration. The **AWS Digital Sovereignty Pledge** and **European (Zurich) region blog** reiterate that **Bedrock keeps data in chosen regions** and complies with EU/UK data transfer requirements.
    

### 4.2 Data in Transit

Data in transit to and from Amazon Bedrock is strongly protected:

- **Encryption in Transit:** All data exchanged with Bedrock’s API endpoints is **encrypted using TLS (SSL)**. AWS **requires TLS 1.2** for all service communications and recommends TLS 1.3. According to AWS documentation, _“Requests to the Amazon Bedrock API and console are made over a secure (SSL) connection”_. This meets UK Government expectations (per NCSC guidance on TLS) that sensitive data should be encrypted in transit with robust protocols.
    
- **AWS Network Security:** When using Bedrock with **PrivateLink (VPC Endpoints)**, the network traffic stays entirely within the AWS global network and **does not traverse the public internet**. Even without PrivateLink, traffic from your VPC to Bedrock’s regional endpoint stays within that AWS region’s infrastructure and is encrypted.
    
- **FIPS Endpoints:** For projects requiring FIPS 140-3 validated cryptography (e.g., certain government standards), AWS provides **FIPS 140-2/3 endpoints** for Bedrock in applicable regions (e.g., `bedrock-fips.us-east-1.amazonaws.com`). The London region (`eu-west-2`) currently does not list a separate FIPS endpoint, but UK teams with FIPS requirements might route via Ireland or rely on AWS’s default encryption modules which are FIPS-validated within AWS’s boundary.
    
- **In-Transit Security Compliance:** AWS’s networking and TLS implementation is compliant with **NCSC Cloud Security Principle #1 (Data in transit protection)**. This means data in transit for Bedrock should be adequately protected against eavesdropping and tampering, satisfying UK OFFICIAL data standards.
    

### 4.3 Data at Rest

For data at rest (storage of any artifacts or logs within Bedrock):

- **Managed Service Data:** Amazon Bedrock is largely stateless regarding prompts, but it will handle data at rest for **model customization artifacts, logs, and any managed knowledge store**. All such data is **encrypted at rest using AWS-managed keys by default**.
    
- **KMS Customer-Managed Keys:** Bedrock allows or automatically leverages **AWS KMS** for certain data at rest:
    
    - **Fine-tuning artifacts and custom models**: These can be encrypted with a customer-managed KMS key (specifiable during job creation).
        
    - **Bedrock Agents data**: Agent configurations can be tied to customer KMS keys.
        
    - **Knowledge Bases (vector stores)**: Data ingestion into Bedrock-managed knowledge stores (e.g., for RAG) supports KMS encryption.
        
    - **S3 Buckets**: Any S3 buckets you integrate (for training data, output storage) can use server-side encryption with AWS-managed or customer-managed KMS keys.
        
- **Storage Locations:** By default, any data at rest remains in the region where the service is used. For example, a fine-tuning job in London will store the model artifact in London (likely in an S3 bucket managed by Bedrock in `eu-west-2`). Ensure that you configure **S3 bucket replication settings off** (or appropriately) if you export data, to maintain residency.
    
- **Data Durability and Deletion:** Bedrock will create resources (custom models, logs) in your AWS account that you can delete or manage. There is no _standing data store of prompts_ in Bedrock (unless you intentionally enable logging to S3/CloudWatch). If a UK government project ends, all Bedrock-created resources can be deleted via the console or APIs, which will also delete the associated data at rest. AWS’s standard practices (and the DPA) ensure that any residual data on underlying storage is eventually purged in accordance with secure data deletion processes.
    
- **Sensitive Data Constraints:** As a best practice, **avoid putting UK OFFICIAL-SENSITIVE data in prompts or fine-tuning datasets unless necessary**, because while Bedrock secures it, the nature of LLMs is such that outputs could inadvertently reveal some input context. If you must, treat the fine-tuned model and any logs as sensitive data assets with restricted access (apply IAM controls and encryption).
    
- **Compliance with UK Gov Standards:** Data at rest encryption in AWS (AES-256 with KMS) meets **ISO 27001** controls and UK government expectations. If handling personal data, it also aligns with GDPR principles of security of processing (Article 32).
    

## 5. Audit Logging

**Audit and activity logging** in Bedrock is robust and integrates with standard AWS logging tools:

- **AWS CloudTrail Integration:** **CloudTrail captures all Amazon Bedrock API calls** as events. This includes calls made via the Bedrock console or programmatically (e.g., `InvokeModel`, `CreateModelCustomizationJob`). By examining CloudTrail logs, an auditor can see **which user/role invoked which model, at what time, from which IP, and what parameters were passed**. For example, a log can show that _User X invoked Anthropic Claude vX model at 10:00 GMT from IP A.B.C.D_. This level of logging is critical for compliance (e.g., evidencing who accessed potentially sensitive models or data).
    
- **CloudTrail Log Retention/Export:** Agencies can **set up a Trail** to deliver these logs to an S3 bucket for long-term retention. By default, recent events are viewable in CloudTrail for 90 days. An S3-backed trail enables storage for **7+ years** or per agency policy. These logs can also feed into AWS CloudWatch or SIEM tools for real-time monitoring.
    
- **CloudWatch Invocation Logging:** Bedrock provides an **Invocation Logging** feature to capture **full request and response payloads and metadata** to CloudWatch Logs or S3 ([Secure Gen AI Apps - Amazon Bedrock Security and Privacy - AWS](https://aws.amazon.com/bedrock/security-compliance/#:~:text=Amazon%20Bedrock%20offers%20comprehensive%20monitoring,Bedrock%20implements%20automated%20abuse%20detection)). This is useful if you need to **audit the content of prompts and outputs** for compliance or debugging. Caution: enabling this means sensitive text might be stored in logs. AWS allows directing these logs to a customer-controlled S3 bucket, which should be encrypted and access-controlled.
    
- **Monitoring and Metrics:** **Amazon CloudWatch** can track Bedrock usage metrics (e.g., number of invocations, latency, errors) ([Secure Gen AI Apps - Amazon Bedrock Security and Privacy - AWS](https://aws.amazon.com/bedrock/security-compliance/#:~:text=Amazon%20Bedrock%20offers%20comprehensive%20monitoring,to%20prevent%20potential%20misuse%2C%20Amazon)). These metrics can inform audit reviews (e.g., unusual spikes in usage could indicate misuse).
    
- **Access to Logs:** UK Government security analysts can access CloudTrail logs via the AWS Console (CloudTrail section) or retrieve the JSON log files from S3. CloudWatch Logs (if used for invocation logging) can be queried in the Console or via CLI/SDK. **Logs can be exported** (e.g., from CloudWatch to S3) for offline analysis or to integrate with central government log management systems.
    
- **Retention and Sovereignty:** By configuring the S3 bucket’s region (e.g., keeping it in the UK), you ensure that audit logs are stored in the UK. CloudTrail supports multi-region trails, but for sovereignty, one might restrict logging to the same region as Bedrock usage.
    
- **Automated Abuse Alerts:** AWS Bedrock’s **automated abuse detection** might generate **CloudWatch Events or GuardDuty findings** if suspicious content is detected. While not explicitly detailed in Bedrock docs, this aligns with AWS services raising flags on policy violations. Such events would be part of an audit trail showing AWS’s enforcement actions (if any).
    

In summary, AWS Bedrock offers comprehensive audit logging through CloudTrail and optional detailed logging, allowing UK government users to meet accountability and monitoring requirements (e.g., supporting the NCSC principle of _Audit and monitoring_).

## 6. Access Controls

Bedrock leverages AWS’s Identity and Access Management (IAM) for **fine-grained access control**:

- **IAM Policies for Bedrock:** Administrators can use IAM to control who (which IAM users/roles) can perform Bedrock actions. Key Bedrock API actions include:
    
    - _`bedrock:InvokeModel`_, _`bedrock:InvokeAgent`_: invoke a foundation model or agent.
        
    - _`bedrock:CreateModelCustomizationJob`_: fine-tune a model.
        
    - _`bedrock:Get*` and `List*` operations_: retrieve details about models, jobs, etc.
        
    
    Using IAM, you can **deny or allow Bedrock actions** to specific roles. For example, a policy could allow data scientists to fine-tune models but deny them the ability to invoke certain foundation models unless authorized.
    
- **Model-Level Access Control:** Bedrock has a concept of **“Model Access”** settings. By default, some third-party models require you to explicitly enable access via the Bedrock console (often by agreeing to the model’s terms or describing your use case). Once enabled, the model becomes usable by any IAM principal in the account (there isn’t per-user model access within the same AWS account). However, you _can_ implement model-level restrictions via IAM policies: since each model invocation uses a specific `ModelId`, you can write IAM conditions to **allow or deny `bedrock:InvokeModel` on particular model ARNs**. For instance, you might restrict a particularly powerful model (like Claude 2) to only a subset of users by denying others access to that model ID.
    
- **AWS IAM Identity Center (SSO):** If the UK Gov organisation uses AWS SSO/Identity Center or federated AD login, those identities can assume IAM roles with Bedrock permissions. This ensures strong authentication (MFA enforced via SSO) for accessing Bedrock.
    
- **Network Controls:** In addition to identity controls, Bedrock can be accessed through **VPC Endpoints**, meaning you could restrict Bedrock usage to only happen from within certain secured networks. For example, you could use VPC endpoint policies to only allow Bedrock API calls from a specific subnet (though typically IAM is the primary control).
    
- **Best Practices by AWS:** AWS recommends **least privilege** for IAM – e.g., if an application only needs to invoke a specific Bedrock model, its IAM role should only have permission for that action and model. They also suggest using **MFA** and individual accounts for better accountability. For highly sensitive projects, consider requiring human approvals or use case justification (outside of AWS) before granting access to Bedrock’s powerful models.
    
- **Multi-Account Strategies:** In larger architectures, one might separate Bedrock usage into a dedicated AWS account and use **RAM (Resource Access Manager)** or cross-account IAM roles to allow other accounts to invoke Bedrock. This way, all Bedrock activity is isolated and easier to monitor. The downside is complexity; small teams can simply use IAM users/roles in one account.
    
- **Model Deployment Accounts (Under the hood):** AWS mentions that Bedrock uses internal “model deployment accounts” for each model provider. **This is transparent to customers** but reassuring: model providers (like Anthropic) only deliver the model to AWS, and AWS then deploys it in an account controlled by AWS. **Model providers have no access** to these accounts or to customer data being processed. So from an access standpoint, **only the customer and AWS operations staff** have access to the runtime. AWS staff access is governed by SOC controls and monitored as per standard AWS cloud practices.
    
- **Temporary Credentials & Logging:** If using Bedrock from applications, prefer to use **IAM roles with temporary credentials** (e.g., EC2 roles or AWS STS assume-role) to avoid long-term static credentials. CloudTrail will then log which role used Bedrock, aiding traceability.
    

## 7. Compliance and Regulatory Requirements

AWS Bedrock and its underlying infrastructure adhere to a broad set of compliance standards. For UK government use, the most relevant include:

- **UK GDPR / Data Protection Act 2018:** AWS acts as a data processor under the GDPR for services like Bedrock. AWS confirms that **customers can use Bedrock in compliance with GDPR**. The AWS **Global Data Processing Addendum** (incorporating UK GDPR requirements and Standard Contractual Clauses) applies automatically. This ensures lawfulness of any personal data processing in Bedrock.
    
- **ISO 27001 (Information Security Management):** Bedrock is in scope for ISO 27001, as well as related standards **ISO 27017 (Cloud Security), ISO 27018 (Cloud Privacy for PII), ISO 27701 (Privacy Information Management)**. UK government often leans on ISO 27001 certification as an indicator of good security practice.
    
- **SOC 2 and SOC 3:** Bedrock was added to AWS’s SOC 1, SOC 2, and SOC 3 audits (Type II) as of August 15, 2023. These Service Organization Control reports are available via AWS Artifact, providing third-party audited assurances of security controls. While SOC reports are US standards, they are recognized internationally (and can help with UK auditing requirements).
    
- **Cyber Essentials Plus (CE+):** AWS has achieved **Cyber Essentials Plus** certification for its UK infrastructure and services (certificate valid through March 22, 2025). CE+ is a UK Government-backed scheme; AWS’s certification scope covers the AWS UK, Ireland, and Germany corporate infrastructure. This indicates AWS meets baseline security controls expected by UK MoD/Government for cloud services. (Note: CE+ covers AWS as a provider, but customers must still use AWS securely).
    
- **NCSC Cloud Security Principles Alignment:** AWS has published guidance mapping their controls to the **14 NCSC Cloud Security Principles**. Bedrock, as an AWS service, inherits those platform controls (e.g., data in transit protection, asset protection, operational security). UK architects should review the AWS whitepaper “Using AWS in the context of NCSC UK’s Cloud Security Principles” for detailed assurance.
    
- **ISO 9001 (Quality Management):** Bedrock being ISO 9001 certified ([Data Protection and Responsible use of Amazon Bedrock in Switzerland | AWS in Switzerland and Austria (Alps)](https://aws.amazon.com/blogs/alps/security_bedrock/#:~:text=Artifact%20,Bedrock%20Security%20and%20Privacy%20page)) suggests AWS has mature processes, which can be relevant for agencies requiring quality management (e.g., certain procurement standards).
    
- **CSA STAR Level 2:** Amazon Bedrock is **CSA STAR Level 2** certified ([Data Protection and Responsible use of Amazon Bedrock in Switzerland | AWS in Switzerland and Austria (Alps)](https://aws.amazon.com/blogs/alps/security_bedrock/#:~:text=Artifact%20,Bedrock%20Security%20and%20Privacy%20page)), which is the Cloud Security Alliance’s third-party assessment of security. This adds another layer of trust, as CSA STAR Level 2 includes an ISO 27001 certification plus additional cloud-specific controls.
    
- **FedRAMP (US Government standard):** While not directly applicable to UK, it’s noteworthy that Bedrock is **FedRAMP Moderate authorized (and FedRAMP High in GovCloud US-West)**. This indicates rigorous US public sector security standards are met, which by extension implies strong controls. UK customers might reference this as evidence but should rely more on ISO and UK certifications.
    
- **HIPAA Eligibility:** Bedrock is HIPAA eligible, meaning it can be used for healthcare data in the US under a Business Associate Agreement. For UK health sector (NHS) use, while HIPAA itself isn’t required, this shows that Bedrock can handle personal health information under strict regulations. NHS and health agencies would map this to UK’s DSP Toolkit requirements.
    
- **UK Sovereignty and LEGAL Compliance:** AWS has stated that **no additional action is required for generative AI use beyond existing AWS agreements**. UK customers benefit from AWS’s commitments in the **AWS GDPR Center** and **UK-specific addenda**. For example, AWS offers a _UK SCC Addendum_ attached to the DPA for international transfers.
    
- **Cybersecurity Act & Supply Chain:** AWS services including Bedrock also comply with **ISO 22301 (Business Continuity)** and **ISO 20000 (Service Management)** ([Data Protection and Responsible use of Amazon Bedrock in Switzerland | AWS in Switzerland and Austria (Alps)](https://aws.amazon.com/blogs/alps/security_bedrock/#:~:text=Artifact%20,Bedrock%20Security%20and%20Privacy%20page)). These can be relevant for ensuring service reliability and support, which government might require contractually.
    
- **Attestations:** UK government frameworks like **OFFICIAL (including OFFICIAL-SENSITIVE)** don’t have formal “certifications”, but AWS can provide a **Security Assertion** or independent assessment that deploying on Bedrock/AWS meets those requirements when configured correctly. Often, system accreditors will use the above certifications plus architecture review to approve Bedrock for specific use cases.
    

Government users should obtain the latest AWS compliance reports via **AWS Artifact** for due diligence. It’s also recommended to check if AWS Bedrock is on any **UK Government approved supplier lists** (e.g., G-Cloud Digital Marketplace) and review the terms under which it’s offered for public sector procurement.

## 8. References

- Amazon Web Services, **“Data protection – Amazon Bedrock,”** AWS Documentation, [docs.aws.amazon.com](https://docs.aws.amazon.com/bedrock/latest/userguide/data-protection.html), accessed 01 April 2025.
    
- Amazon Web Services, **“Amazon Bedrock Security and Privacy,”** AWS Bedrock Product Page – Security & Compliance section, [aws.amazon.com/bedrock/security-compliance](https://aws.amazon.com/bedrock/security-compliance/), accessed 01 April 2025.
    
- Margo Cronin & Markus Rollwagen, **“Data Protection and Responsible use of Amazon Bedrock in Switzerland,”** AWS Security & Compliance Blog, 07 Nov 2024.
    
- Amazon Web Services, **AWS Service Terms – Section 50.12 (Amazon Bedrock)**, [aws.amazon.com/service-terms](https://aws.amazon.com/service-terms/), accessed 01 April 2025.
    
- Amazon Web Services, **“Privacy Notice – AWS,”** updated 21 Feb 2025, [aws.amazon.com/privacy](https://aws.amazon.com/privacy/), accessed 01 April 2025.
    
- Amazon Web Services, **“Supported foundation models in Amazon Bedrock,”** AWS Documentation, [docs.aws.amazon.com](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html), accessed 01 April 2025.
    
- Swami Sivasubramanian, **“Announcing New Tools to Help Every Business Embrace Generative AI,”** AWS Machine Learning Blog, 28 Sep 2023.
    
- Amazon Web Services, **“Amazon Bedrock FAQs – Data security and compliance,”** [aws.amazon.com/bedrock/faqs](https://aws.amazon.com/bedrock/faqs/), accessed 01 April 2025.
    
- Amazon Web Services, **“Data encryption – Amazon Bedrock,”** AWS Documentation, [docs.aws.amazon.com](https://docs.aws.amazon.com/bedrock/latest/userguide/data-encryption.html), accessed 01 April 2025.
    
- Amazon Web Services, **“Monitor Amazon Bedrock API calls using CloudTrail,”** AWS Documentation, [docs.aws.amazon.com](https://docs.aws.amazon.com/bedrock/latest/userguide/logging-using-cloudtrail.html), accessed 01 April 2025.
    
- Amazon Web Services, **“Add or remove access to Amazon Bedrock foundation models,”** AWS Documentation, [docs.aws.amazon.com](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access-modify.html), accessed 01 April 2025.
    
- Tariro Dongo, **“AWS completes the 2024 Cyber Essentials Plus certification,”** AWS Security Blog, 29 May 2024.
    
- Amazon Web Services, **“Cyber Essentials Plus – AWS Compliance Programs,”** [aws.amazon.com/compliance/cyber-essentials-plus](https://aws.amazon.com/compliance/cyber-essentials-plus/), accessed 01 April 2025.
    
- Amazon Web Services, **“Amazon Bedrock endpoints and quotas – AWS General Reference,”** [docs.aws.amazon.com](https://docs.aws.amazon.com/general/latest/gr/bedrock.html), accessed 01 April 2025.
    
- Amazon Web Services, **“Data Privacy FAQ – AWS Trust Center,”** [aws.amazon.com/compliance/data-privacy-faq](https://aws.amazon.com/compliance/data-privacy-faq), accessed 01 April 2025. (Provides additional information on AWS’s handling of customer content and data privacy commitments)