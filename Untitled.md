# Feature-Based Codebase Chunking for Requirements Analysis

Analyze the codebase and chunk it according to product features and functionality. The goal is to create logical, feature-based groups that represent complete product capabilities, regardless of the technical architecture.

## Chunking Guidelines:

1. **Feature-First Approach**: Identify distinct product features or capabilities and group ALL related files together - including models, views, controllers, tests, and configuration specific to that feature.
2. **Complete Feature Representation**: Each chunk should contain everything needed to understand that feature's requirements, including:
    - Data models and schemas
    - Business logic and services
    - User interface components
    - API endpoints and controllers
    - Feature-specific utilities
    - Tests related to the feature
    - Feature-specific assets or resources
3. **Cross-Cutting Concerns**: Create separate chunks for technical capabilities that support multiple features:
    - Authentication/Authorization
    - Core infrastructure
    - Database abstractions
    - Shared UI components
    - Common utilities
    - Configuration/Build systems
4. **Naming Clarity**: Name each chunk based on what the feature does from a user perspective (e.g., "Document_Upload_And_Processing" rather than "FileHandlers").
5. **Completeness Check**: CRITICAL - Ensure EVERY file in the codebase appears in at least one chunk. Files may appear in multiple chunks if they support multiple features.