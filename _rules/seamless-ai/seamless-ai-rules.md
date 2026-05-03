---
api_specs:
- filename: seamless-ai-contacts-openapi.yml
  format: yaml
  label: Seamless.AI Contacts API
  slug: seamless-ai-contacts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seamless-ai/refs/heads/main/openapi/seamless-ai-contacts-openapi.yml
- filename: seamless-ai-companies-openapi.yml
  format: yaml
  label: Seamless.AI Companies API
  slug: seamless-ai-companies-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seamless-ai/refs/heads/main/openapi/seamless-ai-companies-openapi.yml
categories:
- seamless
description: Spectral linting rules defining API design standards and conventions for Seamless.AI.
layout: rules
name: Seamless.AI API Rules
provider_name: Seamless.AI
provider_slug: seamless-ai
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: seamless-ai-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: seamless-ai-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: seamless-ai-summaries-title-case
  severity: warn
- description: API operations should document rate limiting behavior in description
  given: $.paths[*][post]
  name: seamless-ai-rate-limit-docs
  severity: info
- description: POST endpoints must have a requestBody defined
  given: $.paths[*][post]
  name: seamless-ai-request-body-required
  severity: error
- description: Successful responses must define a schema
  given: $.paths[*][*].responses['200'].content['application/json']
  name: seamless-ai-response-200-schema
  severity: warn
- description: All operations should have security defined
  given: $.paths[*][*]
  name: seamless-ai-security-defined
  severity: error
- description: API paths should include version prefix (/v1/)
  given: $.paths
  name: seamless-ai-api-versioned-paths
  severity: warn
rules_file: rules/seamless-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/seamless-ai/refs/heads/main/rules/seamless-ai-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: seamless-ai-rules
source_filename: seamless-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  seamless-ai-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  seamless-ai-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  seamless-ai-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  seamless-ai-rate-limit-docs:\n    description: API operations should document rate limiting behavior in description\n    severity: info\n    given: \"$.paths[*][post]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  seamless-ai-request-body-required:\n    description: POST endpoints must have a requestBody defined\n    severity: error\n    given: \"$.paths[*][post]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  seamless-ai-response-200-schema:\n    description: Successful responses must define a schema\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  seamless-ai-security-defined:\n    description: All operations should have security defined\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  seamless-ai-api-versioned-paths:\n    description: API paths should include version prefix (/v1/)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+/\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/seamless-ai/refs/heads/main/rules/seamless-ai-rules.yml
tags:
- B2B
- Contact Data
- Sales Intelligence
- Prospecting
- Lead Generation
- CRM Enrichment
- Spectral
- Linting
- API Governance
---
