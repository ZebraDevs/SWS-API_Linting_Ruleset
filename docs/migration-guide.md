# Migration Guide: Adopting Zebra Shared Spectral Rules

This guide helps teams adopt the shared Spectral rules in existing API projects.

## Quick Start

### 1. Update Your `.spectral.yml` File

Replace your existing `.spectral.yml` with:

```yaml
extends:
  - "https://raw.githubusercontent.com/zebratechnologies/SWS-API-SHARED_STYLE_RULES/main/.spectral.yml"
  - "spectral:oas"

# Add project-specific overrides here
rules:
  # Example: Change severity of a rule
  # operation-description: warn
  
  # Example: Disable a rule temporarily
  # zebra-response-examples: "off"
```

### 2. Run Initial Assessment

```bash
# Install Spectral CLI if not already installed
npm install -g @stoplight/spectral-cli

# Run against your API specification
spectral lint your-api-spec.yml
```

## Common Migration Issues

### Issue 1: Missing Security Definitions

**Error**: `oas3-security-section-required`

**Fix**: Add security section to your OpenAPI spec:

```yaml
# Add to root level
security:
  - ApiKeyAuth: []

# Add to components section
components:
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-Key
```

### Issue 2: HTTP URLs in Servers

**Error**: `oas3-protocol-https-only`

**Fix**: Update all server URLs to use HTTPS:

```yaml
# Before
servers:
  - url: http://api.example.com

# After  
servers:
  - url: https://api.example.com
```

### Issue 3: Verbs in Paths

**Error**: `oas3-no-verbs-in-paths`

**Fix**: Convert verb-based paths to resource-based:

```yaml
# Before
paths:
  /getUsers:
  /createUser:
  /updateUser/{id}:

# After
paths:
  /users:          # GET for retrieving users
  /users:          # POST for creating users  
  /users/{userId}: # PUT for updating users
```

### Issue 4: Missing API Versioning

**Error**: `version-in-server-or-path`

**Fix**: Add versioning to server URL or paths:

**Option A: Server-level versioning (recommended)**
```yaml
servers:
  - url: https://api.zebra.com/v1
    description: Version 1 API
```

**Option B: Path-level versioning**
```yaml
paths:
  /v1/users:
  /v1/orders:
```

### Issue 5: Snake_case Property Names

**Error**: `properties-camelCase-alphanumeric`

**Fix**: Convert schema properties to camelCase:

```yaml
# Before
components:
  schemas:
    User:
      properties:
        user_name:
          type: string
        created_at:
          type: string

# After
components:
  schemas:
    User:
      properties:
        userName:
          type: string
        createdAt:
          type: string
```

### Issue 6: Missing Operation Documentation

**Error**: `operation-description`, `operation-operationId`

**Fix**: Add required documentation fields:

```yaml
# Before
paths:
  /users:
    get:
      responses:
        '200':
          description: OK

# After
paths:
  /users:
    get:
      summary: Retrieve users
      description: Get a paginated list of all users in the system
      operationId: getUsers
      tags:
        - Users
      responses:
        '200':
          description: Successfully retrieved users
          content:
            application/json:
              schema:
                # ... schema definition
```

## Gradual Migration Strategy

### Phase 1: Fix Critical Issues (Week 1)
- Security-related rules (HTTPS, security schemes)
- Missing required documentation (contact info, descriptions)
- HTTP method violations

### Phase 2: Address Structure Issues (Week 2)
- Path naming and structure
- Versioning implementation
- Content type standardization

### Phase 3: Improve Documentation (Week 3)
- Add examples to responses
- Enhance schema descriptions
- Complete operation documentation

### Phase 4: Final Polish (Week 4)
- Address remaining warnings
- Review and test against examples
- Update team documentation

## Testing Your Migration

### 1. Validate Against Good Examples
```bash
# Test against the good example
spectral lint examples/good-api.yml
# Should show no errors

# Test against the bad example  
spectral lint examples/bad-api.yml
# Should show multiple violations
```

### 2. Run Against Your API
```bash
# Check your API specification
spectral lint your-api-spec.yml

# Generate detailed report
spectral lint your-api-spec.yml --format=json > spectral-report.json
```

### 3. Integration with CI/CD
Add to your GitHub Actions workflow:

```yaml
- name: Download shared Spectral rules
  run: |
    curl -H "Authorization: token ${{ secrets.GITHUB_TOKEN }}" \
         -H "Accept: application/vnd.github.v3.raw" \
         -o ./zebra-shared-rules.yml \
         https://api.github.com/repos/zebratechnologies/SWS-API-SHARED_STYLE_RULES/contents/.spectral.yml

- name: Run Spectral Linting
  run: spectral lint api-specification.yml
```

## Getting Help

### Internal Resources
- **Confluence**: [Zebra API Style Guide](https://confluence.zebra.com/spaces/SSAS/pages/34043)
- **Team**: Advanced API & Integrations Team
- **Slack**: #api-standards (if available)

### Common Questions

**Q: Can I disable specific rules temporarily?**
A: Yes, add to your `.spectral.yml`:
```yaml
rules:
  rule-name: "off"
```

**Q: How do I override rule severity?**
A: Add to your `.spectral.yml`:
```yaml
rules:
  rule-name: warn  # or error, info, hint
```

**Q: When do I need to update to new rule versions?**
A: The shared ruleset follows semantic versioning. Minor updates are backward compatible, major updates may introduce breaking changes.

## Success Metrics

Track your migration progress:
- [ ] Zero critical security violations
- [ ] All operations have required documentation
- [ ] Consistent naming conventions applied
- [ ] API versioning implemented
- [ ] All responses properly typed
- [ ] Examples provided for key operations

## Next Steps

After successful migration:
1. Set up automated Spectral checks in CI/CD
2. Train team members on new standards
3. Create project-specific rule customizations if needed
4. Contribute back improvements to shared ruleset