# C# Backend Instructions — Example

This is an example scoped instruction file for C# backend code. It activates when Copilot is working on C# files. Copy it into `.github/instructions/csharp-backend.instructions.md` in your repository.

> **Note:** .NET is Defra's secondary stack — Node.js is the primary choice. Use .NET where there is a justified need, such as Microsoft ecosystem integration (Dynamics 365), CPU-intensive backend processing, or large-scale multi-layer services. .NET/C# must only be used for backend services and APIs — do NOT use .NET for frontend applications or user interfaces.

## Example file contents

The content below goes into your `.github/instructions/csharp-backend.instructions.md` file:

---

````markdown
---
applyTo: "**/*.cs,**/*.csproj"
---

# C# Backend

## Language and runtime

- Use the latest LTS version of .NET (currently .NET 10)
- Use modern C# features — pattern matching, records for immutable data, nullable reference types
- Enable nullable reference types (`<Nullable>enable</Nullable>` in csproj)
- Enable implicit usings (`<ImplicitUsings>enable</ImplicitUsings>` in csproj)
- Use `async`/`await` for all asynchronous operations — do not use `.Result` or `.Wait()`
- Follow Microsoft's official C# coding conventions for naming, formatting, and style
- Prefer `var` for local variables when the type is obvious from the right-hand side
- Use containerisation with Doocker

## Framework

- Use ASP.NET Core Minimal APIs for new services — do not use MVC controllers unless migrating legacy code
- Register endpoints using `MapGet`, `MapPost`, `MapPut`, `MapDelete` extension methods
- Use the built-in ASP.NET Core dependency injection container
- Do not develop frontend applications in .NET — use Node.js with Nunjucks for frontends

### Endpoint structure

Organise endpoints as static extension methods grouped by domain area:

✅ Minimal API endpoint:
```csharp
public static class ApplicationEndpoints
{
    public static IEndpointRouteBuilder MapApplicationEndpoints(
        this IEndpointRouteBuilder app)
    {
        app.MapGet("/applications/{id}", async (
            string id,
            IApplicationService applicationService) =>
        {
            var application = await applicationService.GetByIdAsync(id);
            return application is not null
                ? Results.Ok(application)
                : Results.NotFound();
        });

        return app;
    }
}
```

❌ Do not use MVC controller patterns in new services:
```csharp
// Wrong — use Minimal APIs instead
[ApiController]
[Route("api/[controller]")]
public class ApplicationsController : ControllerBase
{
    [HttpGet("{id}")]
    public async Task<IActionResult> Get(string id) { /* ... */ }
}
```

## Architecture

- Follow SOLID principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion)
- Keep endpoint handlers thin — validate input, call a service, return a result
- Business logic belongs in service classes, not endpoint handlers
- Use records for data transfer objects (DTOs) and value objects
- Register all services and dependencies in the DI container at startup

```
Config/           # Server and environment configuration
Endpoints/        # Minimal API endpoint registrations
Models/           # Domain models and DTOs (prefer records)
Services/         # Business logic — called by endpoint handlers
Validators/       # FluentValidation validators
Utils/            # Shared utility code
```

## Validation

- Use FluentValidation for request validation
- Register validators in the DI container
- Return structured error responses with field-level detail
- Validate all user input before processing

✅ Validator example:
```csharp
public class CreateApplicationValidator : AbstractValidator<CreateApplicationRequest>
{
    public CreateApplicationValidator()
    {
        RuleFor(x => x.Name)
            .NotEmpty()
            .MaximumLength(200);

        RuleFor(x => x.Reference)
            .NotEmpty()
            .Matches(@"^[A-Z]{2}\d{6}$")
            .WithMessage("Reference must be two letters followed by six digits");
    }
}
```

## Error handling

- Use `Results.Problem()` for structured error responses
- Return appropriate HTTP status codes (400, 404, 500)
- Return useful error messages without leaking internals (no stack traces, no connection strings)
- Log the full exception server-side for debugging
- Use global exception handling middleware for unhandled exceptions

## Logging

- Use Serilog for structured logging in Elastic Common Schema (ECS) format
- Configure Serilog via `appsettings.json` using `Serilog.Settings.Configuration`
- Log levels: `Fatal`, `Error`, `Warning`, `Information`, `Debug`, `Verbose`
- Never log PII: no names, addresses, emails, phone numbers, NI numbers, bank details, API keys, or tokens
- Include correlation IDs for request tracing — use header propagation middleware
- Set appropriate log levels per environment:
  - Development: `Debug`
  - Staging: `Warning` and above
  - Production: `Error` and above

## Security

- Follow OWASP Secure Coding Practices and Microsoft Secure Coding Guidelines
- Validate and sanitise all user input using FluentValidation
- Use parameterised queries — never concatenate user input into queries
- Never commit secrets to source control — use environment variables or a secrets manager
- Set security headers: `X-Content-Type-Options: nosniff`, `Referrer-Policy: no-referrer`, HSTS
- Do not use `dynamic` types for user-supplied data
- Avoid reflection on user-supplied type names

## Database access

- Use MongoDB.Driver for MongoDB access (CDP platform default)
- For SQL databases, use Entity Framework Core or Dapper with parameterised queries
- Set connection timeouts and configure connection pooling
- Use repository or service patterns — do not access the database directly from endpoint handlers
- Index frequently queried fields

## Environment and configuration

- Load all configuration from environment variables or `appsettings.json`
- Never hard-code secrets, connection strings, or API keys
- Use the ASP.NET Core configuration system (`IConfiguration`) with environment-specific overrides
- Validate required configuration at startup — fail fast if critical values are missing
- Use the Options pattern (`IOptions<T>`) for typed configuration

## Health checks

- Expose a health endpoint at `/health` — this is a CDP platform requirement
- Include checks for database connectivity and critical downstream dependencies
- Return `200 OK` when healthy, appropriate error codes when degraded

## Testing

- Use xUnit v3 as the test framework
- Use FluentAssertions for readable assertions
- Use NSubstitute for mocking dependencies
- Use `Microsoft.AspNetCore.Mvc.Testing` for integration tests
- Unit test coverage must be 90% minimum — do not decrease existing coverage
- Test behaviour, not implementation details
- Mock external dependencies (APIs, databases)
- Use `[ExcludeFromCodeCoverage]` only on infrastructure/bootstrapping code, never on business logic

✅ Test example:
```csharp
public class ApplicationServiceTests
{
    private readonly IApplicationRepository _repository = Substitute.For<IApplicationRepository>();
    private readonly ApplicationService _sut;

    public ApplicationServiceTests()
    {
        _sut = new ApplicationService(_repository);
    }

    [Fact]
    public async Task GetByIdAsync_WhenApplicationExists_ReturnsApplication()
    {
        // Arrange
        var expected = new Application { Id = "123", Name = "Test" };
        _repository.GetByIdAsync("123").Returns(expected);

        // Act
        var result = await _sut.GetByIdAsync("123");

        // Assert
        result.Should().BeEquivalentTo(expected);
    }
}
```

## Code style (editorconfig)

- 4-space indentation, UTF-8 encoding
- Allman brace style (opening braces on new lines)
- Private fields: `_camelCase` prefix
- Static private fields: `s_camelCase` prefix
- Constants: `PascalCase`
- Use predefined types (`int`, `string`) over framework types (`Int32`, `String`)
- Explicit accessibility modifiers required for non-interface members

## Containers and deployment

- Use Defra base images: `defradigital/dotnetcore` for production, `defradigital/dotnetcore-development` for development
- Linux containers always — do not target Windows containers
- Run containers as non-root
- Use Docker multi-stage builds: build → test → publish → production
- Tag images with semver (match the application version)
- Do not store secrets in Docker images or environment files committed to source
- Use Docker Compose for local development

## Dependencies

- Use NuGet for package management
- Keep `packages.lock.json` in version control if using locked mode
- Use only packages with OSI-approved licences compatible with the Open Government Licence
- Do not use packages without a licence
- Run security scanning and resolve vulnerabilities before merging
- Configure Dependabot for automated dependency updates

## Licence

All code is published under the [Open Government Licence v3](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) unless an exception is approved.

## References

- [Defra .NET standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/net_standards.md)
- [Defra C# coding standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/csharp_coding_standards.md)
- [Defra common coding standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/common_coding_standards.md)
- [Defra logging standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/logging_standards.md)
- [Defra security standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/security_standards.md)
- [Defra container standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/container_standards.md)
- [CDP .NET backend template](https://github.com/DEFRA/cdp-dotnet-backend-template)
- [Microsoft C# coding conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)
````

---

[Back to instructions index]({{ "/tool-setup/github-copilot/instructions" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})
