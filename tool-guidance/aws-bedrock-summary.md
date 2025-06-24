# Amazon Bedrock – Summary

This summary covers the key points from the [detailed guide](aws-bedrock-detailed.md). Use it to understand how Amazon Bedrock can work in government environments.

## What Amazon Bedrock does

Amazon Bedrock is a cloud service that gives you access to AI models from companies like Anthropic and Meta. You run it on AWS infrastructure, using the security and compliance features you already have.

You can deploy Bedrock in different ways:
- **Standard cloud:** Models run in AWS public cloud regions
- **Private connection:** Connect without using the public internet (AWS PrivateLink)
- **Dedicated capacity:** Reserved computing power for consistent performance
- **On your premises:** Run some models in your own data centres (via EKS Anywhere)

## Privacy controls

Bedrock protects your data by default:
- **No model training:** Your data does not train or improve AI models (this is the default setting)
- **Private endpoints:** Keep traffic off the public internet using AWS PrivateLink
- **Health data settings:** Configure the service to handle protected health information (if your account is eligible)
- **Knowledge base privacy:** Control whether your knowledge base data improves the service

## Terms and data ownership

Key legal points:
- **You own your content:** Customer content (inputs and outputs) belongs to you, not AWS
- **Model-specific agreements:** Each AI model may have its own licence terms
- **Data protection compliance:** Standard AWS terms cover GDPR and UK data protection laws
- **Content restrictions:** Terms ban generating illegal or harmful content

## Where your data goes

### Location and residency

- **UK region available:** Process data in AWS Europe (London) region to meet UK data residency needs
- **Regional boundaries:** Data stays in the region you choose, with clear separation between regions
- **Custom models:** Store fine-tuned models in the region where you create them
- **Legal jurisdiction:** London region data follows UK law (though AWS as a US company also follows US requirements)

### Data protection in transit

All communication uses TLS 1.2 or higher encryption. Extra security options include:
- **AWS PrivateLink:** Traffic never goes over the public internet
- **Request signing:** Prevents tampering with API requests
- **Mutual TLS:** Extra encryption layer for sensitive work

### Data protection at rest

- **Standard use:** Bedrock does not store your requests or responses permanently
- **Feature storage:** Fine-tuning data and knowledge bases use AES-256 encryption
- **Key management:** Use AWS KMS to control your own encryption keys
- **Data deletion:** Delete custom models and datasets when you no longer need them

## Audit logs

Bedrock connects to AWS logging systems:
- **CloudTrail:** Records all API calls with user identity, time, source IP, and request details
- **CloudWatch:** Tracks model operations and can optionally log content
- **Guardrails logging:** Monitors policy violations or blocked content when you use content filtering
- **Evaluation results:** Stores model performance data to track changes over time

## Access controls

Bedrock uses multiple security layers:
- **IAM policies:** Role-based access control which actions users can perform on which resources
- **Resource policies:** Attach permissions directly to specific models or resources
- **Organisation policies:** Set permission boundaries across multiple AWS accounts
- **Condition-based access:** Restrict access based on IP address, time, or other factors
- **Network controls:** Use VPC endpoints to control network access to Bedrock

## Compliance and regulation

AWS Bedrock benefits from AWS's compliance programmes:
- **Security certifications:** ISO 27001, SOC 2, CSA STAR covering AWS infrastructure
- **UK government:** Cyber Essentials Plus, alignment with NCSC Cloud Security Principles
- **Data protection:** ISO 27018, UK GDPR compliance through Data Processing Agreements
- **Healthcare:** HIPAA eligibility for certain models and applications
- **AI governance:** Model safety testing, content filtering (Bedrock Guardrails), ongoing evaluation
