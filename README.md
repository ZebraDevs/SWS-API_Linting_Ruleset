# Zebra Technologies Shared API Style Rules

This repository contains the shared Spectral OpenAPI linting rules used across all Zebra Technologies API projects to ensure consistency, quality, and adherence to organizational standards.

## 🎯 Purpose

- **Standardize API Design**: Enforce consistent API design patterns across all Zebra Technologies projects
- **Quality Assurance**: Catch common API design issues early in development
- **Documentation**: Ensure APIs are properly documented and follow OpenAPI best practices
- **Security**: Enforce security standards like HTTPS-only communication
- **Maintainability**: Promote clean, readable API specifications

## 📋 Getting Started

### Using These Rules in Your Project

 - Use this a template: https://github.com/zebratechnologies/SWS-API_Linting_Template


## 🔧 Installation

### Local Prerequisites
- Node.js 16 or higher
- Spectral CLI: `npm install -g @stoplight/spectral-cli`

### Local Testing
1. Clone this repository
2. Run `spectral lint examples/good-api.yml` to test the rules
3. Run `spectral lint examples/bad-api.yml` to see rule violations

## 📖 Rule Categories

### 🔒 Security Rules
- **HTTPS Only**: All server URLs must use HTTPS protocol
- **Security Schemes**: APIs must define security schemes when using authentication

### 📝 Documentation Rules
- **API Information**: Required info section with contact and description
- **Operation Documentation**: All operations must have descriptions and summaries
- **Parameter Documentation**: All parameters must be documented
- **Response Documentation**: All responses must include proper content definitions

### 🏗️ Structure Rules
- **Versioning**: APIs must include version information in URL or path
- **Resource-Focused Paths**: Paths should be noun-based, not verb-based
- **Proper HTTP Methods**: Correct usage of GET, POST, PUT, DELETE methods
- **Request/Response Bodies**: Appropriate use of request and response bodies

### 🎨 Style Rules
- **Naming Conventions**: camelCase for properties, kebab-case for paths
- **Path Structure**: Plural nouns, no file extensions, proper hierarchy
- **Response Formats**: Consistent JSON response formatting

## 📁 Repository Structure

```
.
├── .spectral.yml              # Main shared ruleset
├── README.md                  # This file
├── docs/                      # Additional documentation
│   ├── rule-explanations.md   # Detailed rule explanations
│   └── migration-guide.md     # Guide for adopting these rules
└── examples/                  # Example API specifications
    ├── good-api.yml           # Example of compliant API
    └── bad-api.yml            # Example showing common violations
└── .github/                   # Github folder
    └── workflows/             # Action workflows
        └── spectral-lint.yml  # workflow to run on PR requests
```

## 🔄 Version History

- **v1.0.0**: Initial release with core Zebra Technologies API standards
- See [CHANGELOG.md](./CHANGELOG.md) for detailed version history

## 🤝 Contributing

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/new-rule`
3. Test your changes against example files
4. Submit a pull request with clear documentation

## 📞 Support

- **Internal Documentation**: [Zebra API Style Guide](https://confluence.zebra.com/spaces/SSAS/pages/340435526/REST+API+Style+Guide)
- **Issues**: Report issues via GitHub Issues
- **Contact**: API Management Team: [ES Service Desk](https://jira.zebra.com/servicedesk/customer/portal/5/create/194)

## 📄 License

Internal use only - Zebra Technologies Corporation

---
*This ruleset is maintained by the Zebra Technologies SWS API Management Team*
