---
api_specs:
- filename: springer-nature-meta-openapi.yml
  format: yaml
  label: Springer Nature Meta API
  slug: springer-nature-meta-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/springer-nature/refs/heads/main/openapi/springer-nature-meta-openapi.yml
- filename: springer-nature-openaccess-openapi.yml
  format: yaml
  label: Springer Nature Open Access API
  slug: springer-nature-openaccess-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/springer-nature/refs/heads/main/openapi/springer-nature-openaccess-openapi.yml
categories:
- springer
description: Spectral linting rules defining API design standards and conventions for Springer Nature.
layout: rules
name: Springer Nature API Rules
provider_name: Springer Nature
provider_slug: springer-nature
rule_count: 7
rules:
- description: Springer Nature APIs require API key authentication
  given: $.components
  name: springer-nature-api-key-required
  severity: error
- description: All operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: springer-nature-operation-id
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: springer-nature-tags-required
  severity: warn
- description: Summaries must use Title Case
  given: $.paths[*][*].summary
  name: springer-nature-summary-title-case
  severity: warn
- description: Search endpoints must document q, s, and p parameters
  given: $.paths[*].get
  name: springer-nature-search-parameters
  severity: info
- description: APIs should document 429 rate limit responses
  given: $.paths[*][*]
  name: springer-nature-rate-limit-responses
  severity: warn
- description: Springer Nature API servers must use HTTPS
  given: $.servers[*].url
  name: springer-nature-server-https
  severity: error
rules_file: rules/springer-nature-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/springer-nature/refs/heads/main/rules/springer-nature-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: springer-nature-rules
source_filename: springer-nature-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  springer-nature-api-key-required:\n    description: Springer Nature APIs require API key authentication\n    message: \"API must define security schemes\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  springer-nature-operation-id:\n    description: All operations must have operationId\n    message: \"Missing operationId at {{path}}\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  springer-nature-tags-required:\n    description: All operations must have tags\n    message: \"Operation at {{path}} must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  springer-nature-summary-title-case:\n    description: Summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title\
  \ Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  springer-nature-search-parameters:\n    description: Search endpoints must document q, s, and p parameters\n    message: \"Search endpoint at {{path}} should document pagination parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  springer-nature-rate-limit-responses:\n    description: APIs should document 429 rate limit responses\n    message: \"Rate-limited endpoint should define 429 response at {{path}}\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.429\"\n      function: truthy\n\n  springer-nature-server-https:\n    description: Springer Nature API servers must use HTTPS\n    message: \"Server URL should use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n  \
  \    functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/springer-nature/refs/heads/main/rules/springer-nature-rules.yml
tags:
- Academic Publishing
- Open Access
- Research
- Scholarly Content
- Scientific Publishing
- Spectral
- Linting
- API Governance
---
