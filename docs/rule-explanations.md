# Detailed Rule Explanations

This document provides detailed explanations for each rule in the Zebra Technologies shared Spectral ruleset.

## Security Rules

### `oas3-protocol-https-only`
**Severity**: Error  
**Purpose**: Ensures all API communications are encrypted and secure.  
**Details**: All server URLs must use the HTTPS protocol. HTTP connections are not allowed in production APIs as they expose data in transit to potential interception.

**Example**:
```yaml
# ✅ Good
servers:
  - url: https://api.zebra.com/v1

# ❌ Bad
servers:
  - url: http://api.zebra.com/v1
```

### `oas3-security-section-required`
**Severity**: Error  
**Purpose**: Ensures APIs define their security requirements at the root level.  
**Details**: All APIs must include a security section to indicate which authentication methods are required for API access.

### `oas3-security-schemes-required`
**Severity**: Error  
**Purpose**: Ensures security schemes are properly defined.  
**Details**: When using security, the components section must include securitySchemes that define the available authentication methods.

## Documentation Rules

### `info-contact`
**Severity**: Error  
**Purpose**: Provides contact information for API consumers.  
**Details**: The API info section must include contact details so consumers know who to reach for support or questions.

### `operation-description`
**Severity**: Error  
**Purpose**: Ensures all API operations are properly documented.  
**Details**: Every operation (GET, POST, PUT, DELETE, etc.) must include a description explaining what the operation does.

### `operation-operationId`
**Severity**: Error  
**Purpose**: Enables code generation and operation identification.  
**Details**: Every operation must have a unique operationId that can be used by code generators and tools to create method names.

## Versioning Rules

### `zebra-api-version`
**Severity**: Error  
**Purpose**: Ensures APIs are properly versioned.  
**Details**: The info.version field must be present and contain a valid version number following semantic versioning.

### `version-in-server-or-path`
**Severity**: Error  
**Purpose**: Makes API versioning explicit in the URL structure.  
**Details**: Either the server URL or the path structure must include a version indicator (e.g., /v1/, /v2/) to support API evolution.

## HTTP Method Rules

### `oas3-no-get-request-body`
**Severity**: Error  
**Purpose**: Follows HTTP specification for GET requests.  
**Details**: GET requests should not include request bodies. Use query parameters for filtering and options.

### `oas3-put-with-request-body`
**Severity**: Error  
**Purpose**: Ensures PUT requests follow RESTful conventions.  
**Details**: PUT requests must include a request body containing the resource data to be updated.

## Content Type Rules

### `oas3-request-support-json`
**Severity**: Error  
**Purpose**: Standardizes on JSON for API communications.  
**Details**: All request bodies must support application/json media type for consistency and ease of use.

### `oas3-response-success-json`
**Severity**: Error  
**Purpose**: Standardizes response format.  
**Details**: All successful responses (200-299) must use application/json content type, except for 204 No Content responses.

## Path and Naming Rules

### `paths-kebab-case`
**Severity**: Warning  
**Purpose**: Ensures consistent URL formatting.  
**Details**: API paths should use kebab-case (lowercase with hyphens) for readability and consistency.

### `oas3-no-verbs-in-paths`
**Severity**: Error  
**Purpose**: Promotes resource-oriented API design.  
**Details**: Paths should represent resources (nouns) not actions (verbs). Use HTTP methods to indicate the action.

### `path-should-have-at-least-one-plural-noun`
**Severity**: Error  
**Purpose**: Follows RESTful resource naming conventions.  
**Details**: Paths should include plural nouns to represent collections of resources (e.g., /users, /orders).

### `no-file-extensions-in-paths`
**Severity**: Error  
**Purpose**: Keeps URLs clean and flexible.  
**Details**: Don't include file extensions like .json or .xml in paths. Use the Accept header or content negotiation instead.

## Parameter Naming Rules

### `path-parameters-camelCase-alphanumeric`
**Severity**: Error  
**Purpose**: Ensures consistent parameter naming.  
**Details**: Path parameters must use camelCase naming convention for consistency with JSON property naming.

### `properties-camelCase-alphanumeric`
**Severity**: Error  
**Purpose**: Standardizes JSON property naming.  
**Details**: All JSON schema properties should use camelCase for consistency and compatibility with JavaScript conventions.

## Zebra-Specific Rules

### `zebra-server-description`
**Severity**: Warning  
**Purpose**: Improves API documentation.  
**Details**: Each server entry should include a description explaining its purpose (production, staging, development, etc.).

### `zebra-response-examples`
**Severity**: Warning  
**Purpose**: Enhances API documentation and testing.  
**Details**: Response definitions should include examples to help consumers understand the expected response format.

### `zebra-schema-properties-description`
**Severity**: Warning  
**Purpose**: Improves schema documentation.  
**Details**: Schema properties should include descriptions to help consumers understand the purpose and format of each field.