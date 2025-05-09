# Amazon Bedrock – Summary

This is a high-level summary of the [detailed report](aws-bedrock-detailed-todd.md)

## 1. Tool Overview

Amazon Bedrock is a fully managed generative AI service on AWS that provides access to foundation models (FMs) from leading AI companies. It allows organisations to build AI applications within AWS's cloud infrastructure, leveraging existing security and compliance capabilities.

The service is offered with several deployment options:
- **Standard Cloud Deployment:** Models hosted in AWS public cloud regions
- **AWS PrivateLink:** Private connectivity without internet exposure
- **Dedicated Capacity:** Reserved compute resources for consistent performance
- **On-Premises (via EKS Anywhere):** Deploy some models in your own data centres

## 2. Privacy Settings

Amazon Bedrock offers strong privacy controls:
- **Opt-out of Model Training:** By default, your data is not used to train or improve foundation models
- **Private Endpoints:** Optional access via AWS PrivateLink without exposing traffic to the public internet
- **HIPAA/PHI Settings:** Optional configuration for handling protected health information (for eligible accounts)
- **Knowledge Base Privacy:** Controls whether data in knowledge bases can be used for service improvement

## 3. Terms of Use and Privacy Policy

- **User Content Ownership:** Customer content processed through Bedrock (inputs and outputs) is owned by the customer, not AWS
- **Model-specific EULAs:** Each foundation model may have its own End User License Agreement with additional terms
- **International Data Transfers:** Standard AWS terms address GDPR and UK data protection compliance
- **Content Restrictions:** Terms explicitly prohibit generating illegal or harmful content

## 4. Data Management

### 4.1 Server Location and Data Residency

- **Regional Deployment:** Available in multiple AWS regions, including Europe (London) for UK data residency requirements
- **Regional Isolation:** Data processed in the AWS region you select, with clear boundaries between regions
- **Model Storage:** Custom models and fine-tuning data stored in the region where processing was initiated
- **Legal Jurisdiction:** Data in London region subject to UK law, though AWS as a US company is also subject to US requirements

### 4.2 Data in Transit

All communication with Bedrock APIs is encrypted using TLS 1.2 or higher. Additional security options include:
- **AWS PrivateLink:** Ensures traffic stays within the AWS network and never traverses the public internet
- **API Request Signing:** SigV4 authentication prevents request tampering or replay attacks
- **Mutual TLS:** Optional additional encryption layer for sensitive workloads

### 4.3 Data at Rest

- **Standard Inference:** Bedrock does not persistently store request content or model responses for standard usage
- **Feature Storage:** For fine-tuning, custom models, and knowledge bases, AWS applies encryption at rest using AES-256
- **Key Management:** Integration with AWS KMS allows customer-managed encryption keys for direct control
- **Data Deletion:** Mechanisms provided to delete custom models, fine-tuning datasets, and knowledge bases

## 5. Audit Logging

Bedrock integrates with AWS's logging ecosystem:
- **CloudTrail:** Records all API calls with identity, time, source IP, request parameters, and response elements
- **CloudWatch:** Provides metrics and logs for model inference operations, including optional content logging
- **Guardrails Logging:** Tracks policy violations or blocked content when using content filtering
- **Evaluation Results:** Stores model performance metrics for tracking model drift and compliance

## 6. Access Controls

Bedrock implements a comprehensive approach to access control:
- **IAM Policies:** Role-based access control defining which actions principals can perform on which resources
- **Resource Policies:** Attached directly to Bedrock resources for more specific control
- **Service Control Policies:** Organisation-wide permission boundaries for consistent security
- **Condition Keys:** Fine-grained context-based access using attributes like tags, IP addresses, or time
- **Network Controls:** VPC endpoint policies restricting which principals can access Bedrock

## 7. Compliance and Regulatory Requirements

AWS Bedrock benefits from AWS's extensive compliance programs:
- **Security Certifications:** ISO 27001, SOC 2, CSA STAR covering AWS infrastructure
- **UK Government:** Cyber Essentials Plus, NCSC Cloud Security Principles alignment
- **Data Protection:** ISO 27018, UK GDPR validation via Data Processing Addendums
- **Industry-specific:** HIPAA eligibility for certain models and healthcare applications
- **AI Governance:** Model safety evaluations, content filtering via Bedrock Guardrails, and ongoing evaluation capabilities

## 8. References

- [AWS Compliance Programs](https://aws.amazon.com/compliance/programs/)
- [AWS UK Compliance Resources](https://aws.amazon.com/compliance/uk-compliance/)
- [Amazon Bedrock Responsible AI Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/responsible-ai.html)
- [AWS Bedrock Security Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/security.html) 