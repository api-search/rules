---
api_specs:
- filename: smithery-openapi.json
  format: json
  label: Smithery Registry API
  slug: registry-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smithery/refs/heads/main/openapi/smithery-openapi.json
categories:
- smithery
description: Spectral linting rules defining API design standards and conventions for Smithery.
layout: rules
name: Smithery API Rules
provider_name: Smithery
provider_slug: smithery
rule_count: 8
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: smithery-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: smithery-operation-tags
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smithery-summary-title-case
  severity: warn
- description: API must define Bearer token authentication
  given: $.components.securitySchemes
  name: smithery-bearer-auth
  severity: error
- description: Server paths should use {qualifiedName} parameter for namespace/server identification
  given: $.paths
  name: smithery-qualified-name-paths
  severity: warn
- description: All operations must define at least a 4xx error response
  given: $.paths[*][post,put,patch,delete]
  name: smithery-error-responses
  severity: warn
- description: API paths must not have trailing slashes
  given: $.paths
  name: smithery-no-trailing-slashes
  severity: warn
- description: Request bodies must use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: smithery-content-type-json
  severity: warn
rules_file: rules/smithery-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smithery/refs/heads/main/rules/smithery-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: smithery-rules
source_filename: smithery-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  smithery-operation-ids:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  smithery-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smithery-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  smithery-bearer-auth:\n    description: API must define Bearer token authentication\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  smithery-qualified-name-paths:\n    description: Server paths should use {qualifiedName} parameter for namespace/server identification\n\
  \    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"qualifiedName|namespace|slug\"\n\n  smithery-error-responses:\n    description: All operations must define at least a 4xx error response\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete]\"\n    then:\n      field: responses\n      function: truthy\n\n  smithery-no-trailing-slashes:\n    description: API paths must not have trailing slashes\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  smithery-content-type-json:\n    description: Request bodies must use application/json content type\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smithery/refs/heads/main/rules/smithery-rules.yml
tags:
- Artificial Intelligence
- Large Language Models
- MCP
- Model Context Protocol
- AI Agents
- Developer Tools
- Spectral
- Linting
- API Governance
---
