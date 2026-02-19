# Write Tests Prompt — Example

This is an example `.prompt.md` file for generating test suites. Copy it into `.github/prompts/write-tests.prompt.md` in your repository.

## Example file contents

The content below goes into your `.github/prompts/write-tests.prompt.md` file:

---

````markdown
---
description: Generate a test suite for the selected code
---

# Write Tests

Generate a comprehensive test suite for the selected code. Follow Defra testing standards and quality targets.

## What to test

Analyse the selected code and generate tests covering:

1. **Happy path** — the expected behaviour with valid inputs
2. **Edge cases** — boundary values, empty inputs, minimum and maximum values
3. **Error cases** — invalid inputs, missing dependencies, network failures
4. **Security cases** — malicious input, injection attempts (where applicable)

## Output format

- Use Jest as the test framework
- Save the test file alongside the source file with `.test.js` suffix
  - Example: `src/services/application.js` → `src/services/application.test.js`
- Use `describe` and `it` blocks with descriptive names

## Test structure

```javascript
import { functionName } from './module-name.js'

describe('functionName', () => {
  describe('when given valid input', () => {
    it('should return the expected result', () => {
      // Arrange
      const input = { /* valid data */ }

      // Act
      const result = functionName(input)

      // Assert
      expect(result).toEqual(expectedOutput)
    })
  })

  describe('when given invalid input', () => {
    it('should throw a descriptive error', () => {
      expect(() => functionName(null)).toThrow('Input is required')
    })
  })
})
```

## Rules

- Mock external dependencies (databases, APIs, file system) — do not make real network calls
- Test behaviour, not implementation details
- Each test should be independent — no shared mutable state between tests
- Use `beforeEach` for common setup, not `beforeAll` (unless expensive and read-only)
- Do not use `test.only` or `describe.only` in committed code
- Do not reduce existing test coverage
- Target 90% coverage minimum for new code
- Core business logic must reach 95% coverage
- Error and security paths must reach 100% coverage
- Do not include PII in test fixtures or assertions
````

---

[Back to prompts index]({{ "/tool-setup/github-copilot/prompts" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})
