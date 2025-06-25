# Amazon Q Developer - Summary

**Approval status:** Approved - you can use this tool within Defra when you follow the tool guidance advice.

This summary covers the key points from the [detailed guide](amazon-q-developers-detailed.md). Use it to understand how Amazon Q Developer can work in government environments.

## What Amazon Q Developer does

Amazon Q Developer is a generative AI-powered coding assistant created by AWS. It helps software developers understand, build, and maintain applications on AWS.

### Key capabilities

The tool can:

- provide real-time code suggestions and generate functions
- offer AWS architecture guidance and troubleshooting
- scan code for security vulnerabilities and suggest fixes
- execute multi-step development tasks autonomously
- integrate with popular development environments (VS Code, IntelliJ, Visual Studio)

### Subscription tiers

**Free Tier**: Limited monthly usage with basic features

**Pro Tier**: Enterprise subscription with enhanced data controls and additional features

## Privacy controls

Privacy protections vary significantly between subscription tiers.

### Pro Tier protections

- AWS will not use your content to train AI models for other customers
- Your code and conversations remain private to your organisation
- Data stays within your chosen AWS region

### Free Tier considerations

- AWS may store and use your content to improve the service by default
- You can opt out of this data usage through AWS Organisations policies or IDE settings
- All data is stored in US regions regardless of your location

### Best practices

AWS recommends avoiding highly sensitive or confidential data in prompts, especially on the Free Tier.

## Terms of use and privacy policy

### Contractual framework

Amazon Q Developer operates under:

- AWS Customer Agreement
- AWS Service Terms
- AWS Privacy Notice

### Key differences between tiers

**Free Tier**: 
- AWS may use your prompts and responses for service improvement
- No intellectual property indemnification

**Pro Tier**:
- Excluded from AWS data usage for improvements
- Includes AWS intellectual property indemnification against third-party claims

### Data ownership

You retain ownership of your data. AWS will only access customer content when necessary to provide the service or as required by law.

## Where your data goes

### Multi-regional processing

**Data storage location**:

- **Pro Tier**: Data stored in your chosen AWS region (can select UK or EU regions)
- **Free Tier**: All data stored in US regions (Virginia and Oregon)

**Cross-region inference**:
- Service may process requests across multiple regions within the same geography for performance
- Data remains stored in the primary region
- All cross-region data transfer is encrypted
- Can be disabled via policy if required

### Data protection in transit

All data transmission uses:

- TLS 1.2 or higher encryption
- Encrypted communication between all service components
- Protection against interception during transfer

This meets UK government minimum expectations for transport security.

### Data protection at rest

**Default encryption**:
- All stored data encrypted using AWS Key Management Service (KMS)
- AES-256 encryption standard
- AWS-managed encryption keys used by default

**Enhanced control (Pro Tier)**:
- Option to use customer-managed KMS keys
- Provides "Bring Your Own Key" (BYOK) capability
- You control access to encryption keys

**Data retention**:
- **Active use**: Content retained as needed for service functionality
- **Account termination**: 30-day grace period before deletion
- **Pro Tier**: No long-term storage beyond operational requirements

## Audit logs

### Automatic audit logging

**CloudWatch Logs**:
- All CLI commands executed by Amazon Q are logged
- Cannot be disabled
- Includes user identification, timestamps, and command details

**CloudTrail integration**:
- AWS API calls made by Amazon Q appear in your CloudTrail logs
- Standard AWS audit trail applies
- Shows what actions were triggered and by whom

### Log ownership and control

- All audit logs stored in your AWS account
- You control access to logs through IAM permissions
- Logs can be retained as long as required
- Integration with existing monitoring and SIEM systems possible

## Access controls

### Authentication and authorisation

**User access**:
- Requires AWS identity authentication
- Enterprise integration through AWS IAM Identity Centre (SSO)
- Multi-factor authentication supported and recommended

**Permission framework**:
- Uses AWS IAM for all access control
- Amazon Q cannot exceed the permissions of the calling user
- Managed IAM policy 'AmazonQDeveloperAccess' required for basic usage

### Operational controls

**Role-based operation**:
- Amazon Q operates under configurable IAM roles
- You control what actions it can perform
- Can map individual users to specific roles for accountability

**Guardrails and restrictions**:
- Service Control Policies can restrict capabilities organisation-wide
- Channel-specific guardrail policies available
- Built-in blocks for high-risk operations
- Principle of least privilege enforced

## Compliance and regulation

### Current certifications

**Achieved**:
- UK Cyber Essentials Plus
- CSA STAR (Level 1)
- SOC 1, 2, 3 compliance (confirmed for Amazon Q Business, likely applies to Q Developer)

**Infrastructure inherited**:
- AWS's broader compliance framework applies
- ISO 27017 (cloud security) and ISO 27018 (cloud privacy) through AWS platform

### Pending certifications

**ISO 27001**: Amazon Q Developer not yet explicitly listed in AWS's ISO 27001 scope (expected to be included)

### Data protection compliance

**UK GDPR**:
- AWS Data Processing Agreement covers the service
- Customer data control maintained
- Regional data processing available (Pro Tier)
- Right to deletion supported

**NCSC Cloud Security Principles**: Service design aligns with UK National Cyber Security Centre guidance

### Government suitability

The service appears suitable for UK government use when:
- Pro Tier is used for sensitive development work
- Appropriate data classification is maintained (Official level)
- Strong IAM governance is implemented
- Audit logging is properly configured
