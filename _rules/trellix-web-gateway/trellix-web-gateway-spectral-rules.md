---
api_specs:
- filename: openapi.json
  format: json
  label: Trellix Web Gateway REST API
  slug: ''
  spec_type: OpenAPI
  url: https://docs.trellix.com/api/web-gateway/openapi.json
- filename: trellix-web-gateway-reporting-openapi.yml
  format: yaml
  label: Trellix Web Gateway Reporting API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trellix-web-gateway/refs/heads/main/openapi/trellix-web-gateway-reporting-openapi.yml
- filename: trellix-web-gateway-policy-openapi.yml
  format: yaml
  label: Trellix Web Gateway Policy API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trellix-web-gateway/refs/heads/main/openapi/trellix-web-gateway-policy-openapi.yml
categories:
- twg
description: Spectral linting rules defining API design standards and conventions for Trellix Web Gateway.
layout: rules
name: Trellix Web Gateway API Rules
provider_name: Trellix Web Gateway
provider_slug: trellix-web-gateway
rule_count: 12
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: twg-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: twg-summary-title-case
  severity: warn
- description: All non-login operations must define security requirements
  given: $.paths[?(!@path.match('/login$'))][get,post,put,patch,delete]
  name: twg-security-defined
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: twg-response-200-get
  severity: error
- description: Authenticated operations should define a 401 response
  given: $.paths[*][get,post,put,delete]
  name: twg-response-401-defined
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: twg-tag-defined
  severity: warn
- description: Server URLs with variables must define those variables
  given: $.servers[*].variables[*]
  name: twg-server-variables
  severity: warn
- description: Web Gateway uses session cookie authentication via JSESSIONID
  given: $.components.securitySchemes.cookieAuth
  name: twg-cookie-auth
  severity: info
- description: API paths should use lowercase letters and hyphens
  given: $.paths[*]~
  name: twg-path-kebab-case
  severity: warn
- description: DELETE operations should return 200 or 204
  given: $.paths[*].delete
  name: twg-delete-response
  severity: warn
- description: POST operations that create resources should define a request body
  given: $.paths[*].post
  name: twg-post-request-body
  severity: warn
- description: Configuration endpoints use XML content type
  given: $.paths['/configuration'].get.responses.200.content
  name: twg-xml-content-type
  severity: info
rules_file: rules/trellix-web-gateway-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trellix-web-gateway/refs/heads/main/rules/trellix-web-gateway-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 8
slug: trellix-web-gateway-spectral-rules
source_filename: trellix-web-gateway-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  twg-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  twg-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /()+&-]*$\"\n\n  twg-security-defined:\n    description: All non-login operations must define security requirements\n    message: \"Operation should define security requirements\"\n    severity: error\n    given: \"$.paths[?(!@path.match('/login$'))][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  twg-response-200-get:\n    description:\
  \ All GET operations must define a 200 response\n    message: \"GET operation must define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  twg-response-401-defined:\n    description: Authenticated operations should define a 401 response\n    message: \"Authenticated operation should define 401 Unauthorized\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: responses.401\n      function: defined\n\n  twg-tag-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  twg-server-variables:\n    description: Server URLs with variables must define those variables\n    message: \"Server URL variable must have a default value\"\n    severity: warn\n    given: \"$.servers[*].variables[*]\"\
  \n    then:\n      field: default\n      function: defined\n\n  twg-cookie-auth:\n    description: Web Gateway uses session cookie authentication via JSESSIONID\n    message: \"Security scheme must be cookieAuth using JSESSIONID cookie\"\n    severity: info\n    given: \"$.components.securitySchemes.cookieAuth\"\n    then:\n      function: defined\n\n  twg-path-kebab-case:\n    description: API paths should use lowercase letters and hyphens\n    message: \"Path segment should be lowercase\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)+$\"\n\n  twg-delete-response:\n    description: DELETE operations should return 200 or 204\n    message: \"DELETE should define a 200 or 204 success response\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n\
  \            responses:\n              type: object\n\n  twg-post-request-body:\n    description: POST operations that create resources should define a request body\n    message: \"POST operation should define a requestBody\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  twg-xml-content-type:\n    description: Configuration endpoints use XML content type\n    message: \"Configuration endpoints should support application/xml\"\n    severity: info\n    given: \"$.paths['/configuration'].get.responses.200.content\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trellix-web-gateway/refs/heads/main/rules/trellix-web-gateway-spectral-rules.yml
tags:
- Cybersecurity
- Data Loss Prevention
- Enterprise Security
- Malware Protection
- Network Security
- SSL Inspection
- Threat Protection
- URL Filtering
- Web Gateway
- Spectral
- Linting
- API Governance
---
