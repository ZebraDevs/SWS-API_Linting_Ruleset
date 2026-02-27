# Changelog

All notable changes to the Zebra Technologies Shared Spectral Rules will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial repository setup
- Comprehensive documentation and examples

## [1.0.0] - 2025-11-13

### Added
- Initial release of shared Spectral rules for Zebra Technologies
- Security rules enforcing HTTPS and proper authentication
- Documentation rules for comprehensive API specifications  
- Versioning requirements for API evolution
- HTTP method best practices
- Content type standardization (JSON-first)
- Path and naming convention enforcement
- Zebra-specific organizational standards

### Security Rules
- `oas3-protocol-https-only`: Enforce HTTPS-only communication
- `oas3-security-section-required`: Require security definitions
- `oas3-components-required`: Require components section
- `oas3-security-schemes-required`: Require security schemes

### Documentation Rules
- `info-contact`: Require API contact information
- `info-description`: Require API description
- `operation-description`: Require operation descriptions
- `operation-operationId`: Require operation IDs
- `operation-operationId-unique`: Ensure unique operation IDs
- `operation-success-response`: Require success responses
- `operation-tag-defined`: Require defined tags
- `zebra-tags-description`: Require tag descriptions
- `response-should-have-body`: Require response content

### Versioning Rules
- `zebra-api-version`: Require version in info section
- `version-in-server-or-path`: Require version in URL structure

### HTTP Method Rules
- `oas3-no-get-request-body`: Prohibit GET request bodies
- `oas3-put-with-request-body`: Require PUT request bodies
- `oas3-not-post-to-get-info`: Discourage POST for data retrieval

### Content Type Rules
- `oas3-request-support-json`: Require JSON support for requests
- `oas3-response-success-json`: Require JSON for success responses

### Path and Naming Rules
- `paths-kebab-case`: Enforce kebab-case for paths
- `oas3-no-verbs-in-paths`: Prohibit verbs in resource paths
- `no-file-extensions-in-paths`: Prohibit file extensions in paths
- `path-should-have-at-least-one-plural-noun`: Require plural resource names
- `path-should-not-include-api`: Prohibit 'api' in path segments
- `path-parameters-camelCase-alphanumeric`: Enforce camelCase path parameters
- `properties-camelCase-alphanumeric`: Enforce camelCase property names

### Zebra-Specific Rules
- `zebra-server-url`: Require server URL specification
- `zebra-server-description`: Require server descriptions
- `zebra-response-examples`: Encourage response examples
- `zebra-schema-properties-description`: Encourage property descriptions

### Documentation
- Comprehensive README with usage instructions
- Detailed rule explanations document
- Migration guide for existing APIs
- Good and bad API specification examples
- Complete project structure and contribution guidelines

---
## [1.0.1] - 2025-12-04

### Minor error fixes
- Fixed issue with version numbers in server or path rule where it was giving an error if the version came at the end of the server path without anything after
- Fixed issue with the plural nouns rule in path where it was erroring if the collection had a dash in it as in /inventory-items
- Updated the github action to fix some formatting errors

---

## Version History Notes

### Version Numbering
- **Major versions** (x.0.0): Breaking changes that may require API specification updates
- **Minor versions** (x.y.0): New rules or enhancements that are backward compatible
- **Patch versions** (x.y.z): Bug fixes and documentation improvements

### Breaking Changes Policy
- Major version changes will be announced at least 30 days in advance
- Migration guides will be provided for all breaking changes
- Previous major versions will be supported for 6 months after new major release

### Contributing Changes
1. Follow semantic versioning principles
2. Update this changelog with your changes
3. Test against both good and bad examples
4. Update documentation as needed
5. Ensure backward compatibility for minor/patch versions
