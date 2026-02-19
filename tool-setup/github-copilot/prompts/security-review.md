# Security Review Prompt — Example

This is an example `.prompt.md` file for reviewing code against security standards. Copy it into `.github/prompts/security-review.prompt.md` in your repository.

## Example file contents

The content below goes into your `.github/prompts/security-review.prompt.md` file:

---

````markdown
---
description: Review selected code against OWASP and Defra security standards
---

# Security Review

Review the selected code for security vulnerabilities. Check against OWASP Secure Coding Practices and Defra security standards.

## Review checklist

Work through each category and report any findings:

### 1. Input validation
- All user input is validated (type, length, range, format)
- Input is sanitised before use in queries, file paths, or HTML output
- Validation happens server-side (client-side validation is not sufficient)

### 2. Authentication and authorisation
- Authentication checks are present on protected routes
- Authorisation verifies the user has permission for the specific resource
- Session tokens are generated securely and have appropriate expiry

### 3. Data protection
- No secrets, API keys, or tokens in source code
- Secrets are loaded from environment variables or a secret manager
- Sensitive data is encrypted in transit (TLS) and at rest
- PII is not logged (names, addresses, emails, phone numbers, NI numbers, bank details)

### 4. Injection prevention
- SQL queries use parameterised statements or an ORM
- No string concatenation in queries, commands, or file paths with user input
- HTML output is escaped to prevent XSS
- HTTP headers include security protections (CSP, X-Frame-Options, HSTS)

### 5. Error handling
- Error messages do not leak internal details (stack traces, SQL queries, file paths)
- Errors are logged server-side with sufficient detail for debugging
- The application fails securely — denied by default on error

### 6. Dependencies
- No known vulnerable dependencies (check `npm audit` or equivalent)
- Dependencies are from trusted sources (npm registry, NuGet)
- Lock file (`package-lock.json`) is committed and up to date

### 7. Logging and monitoring
- Security-relevant events are logged (authentication attempts, access failures, configuration changes)
- Logs do not contain secrets or PII
- Logs include correlation IDs for tracing

## Output format

For each finding, provide:

| Field | Content |
|-------|---------|
| **Severity** | Critical / High / Medium / Low |
| **Category** | Which checklist category |
| **Location** | File and line reference |
| **Description** | What the vulnerability is |
| **Risk** | What could happen if exploited |
| **Recommendation** | How to fix it with a code example |

Summarise at the end: total findings by severity and the overall risk assessment.

## References

- [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Defra security standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/security_standards.md)
- [Defra logging standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/logging_standards.md)
- [NCSC secure development principles](https://www.ncsc.gov.uk/collection/developers-collection)
````

---

[Back to prompts index]({{ "/tool-setup/github-copilot/prompts" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})
