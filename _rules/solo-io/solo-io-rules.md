---
api_specs:
- filename: solo-io-gloo-portal-server-api-openapi.yml
  format: yaml
  label: Solo.io Gloo Portal Server API
  slug: gloo-portal-server-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/openapi/solo-io-gloo-portal-server-api-openapi.yml
- filename: solo-io-gloo-gateway-management-api-openapi.yml
  format: yaml
  label: Solo.io Gloo Gateway Management API
  slug: gloo-gateway-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/openapi/solo-io-gloo-gateway-management-api-openapi.yml
categories:
- solo
description: Spectral linting rules defining API design standards and conventions for Solo.io.
layout: rules
name: Solo.io API Rules
provider_name: Solo.io
provider_slug: solo-io
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: solo-io-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: solo-io-operation-id-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: solo-io-tags-required
  severity: warn
- description: Resource paths should use namespace and name path parameters
  given: $.paths
  name: solo-io-namespace-name-path-params
  severity: info
- description: All GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: solo-io-200-response-required
  severity: error
- description: Successful responses must include a schema
  given: $.paths[*][get,post].responses[200,201].content
  name: solo-io-response-schema-required
  severity: warn
- description: Operations accessing user data must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: solo-io-security-defined
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: solo-io-kebab-case-paths
  severity: warn
- description: Authentication must use bearer token scheme consistent with Solo.io OIDC
  given: $.components.securitySchemes
  name: solo-io-bearer-auth-scheme
  severity: info
rules_file: rules/solo-io-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/rules/solo-io-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: solo-io-rules
source_filename: solo-io-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  solo-io-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\\s[A-Z][a-z]*)*$\"\n\n  solo-io-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  solo-io-tags-required:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  solo-io-namespace-name-path-params:\n    description: Resource paths should use\
  \ namespace and name path parameters\n    message: >-\n      Gloo resource paths should use {namespace}/{name} pattern for individual\n      resource access\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\"\n\n  solo-io-200-response-required:\n    description: All GET operations must have a 200 response\n    message: GET operation must define a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  solo-io-response-schema-required:\n    description: Successful responses must include a schema\n    message: Response 200/201 must include a content schema\n    severity: warn\n    given: \"$.paths[*][get,post].responses[200,201].content\"\n    then:\n      function: truthy\n\n  solo-io-security-defined:\n    description: Operations accessing user data must define security requirements\n    message: Operation should define security requirements\n\
  \    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  solo-io-kebab-case-paths:\n    description: Path segments must use kebab-case\n    message: Path segment \"{{value}}\" must use kebab-case (lowercase with hyphens)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-zA-Z]+\\\\}))*$\"\n\n  solo-io-bearer-auth-scheme:\n    description: Authentication must use bearer token scheme consistent with Solo.io OIDC\n    message: Security scheme must be bearerAuth or apiKeyAuth\n    severity: info\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/rules/solo-io-rules.yml
tags:
- AI Gateway
- Analytics
- Automation
- Gateways
- Management
- Monetization
- Observability
- Platform
- Resiliency
- Security
- Service Mesh
- Traffic Control
- Spectral
- Linting
- API Governance
---
