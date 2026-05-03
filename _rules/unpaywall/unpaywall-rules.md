---
api_specs:
- filename: unpaywall-openapi.yml
  format: yaml
  label: Unpaywall API
  slug: unpaywall
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unpaywall/refs/heads/main/openapi/unpaywall-openapi.yml
categories:
- unpaywall
description: Spectral linting rules defining API design standards and conventions for Unpaywall.
layout: rules
name: Unpaywall API Rules
provider_name: Unpaywall
provider_slug: unpaywall
rule_count: 6
rules:
- description: All Unpaywall API paths must start with /v2/
  given: $.servers[*].url
  name: unpaywall-path-versioning
  severity: info
- description: The email query parameter is required for all Unpaywall API calls
  given: $.paths[*][get]
  name: unpaywall-email-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: unpaywall-title-case-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: unpaywall-operation-id
  severity: error
- description: DOI lookup must define 404 response
  given: $.paths[/{doi}][get]
  name: unpaywall-doi-not-found
  severity: warn
- description: Unpaywall API is read-only and uses GET requests only
  given: $.paths[*][post,put,patch,delete]
  name: unpaywall-get-only
  severity: warn
rules_file: rules/unpaywall-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unpaywall/refs/heads/main/rules/unpaywall-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 3
slug: unpaywall-rules
source_filename: unpaywall-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n\n  # All paths must be versioned with /v2/\n  unpaywall-path-versioning:\n    description: All Unpaywall API paths must start with /v2/\n    message: \"Path should include version prefix\"\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v2$\"\n\n  # Email parameter required for all operations\n  unpaywall-email-required:\n    description: The email query parameter is required for all Unpaywall API calls\n    message: \"Operation must include required email query parameter\"\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      field: parameters\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: email\n              in:\n                const: query\n              required:\n      \
  \          const: true\n\n  # Summaries must be Title Case\n  unpaywall-title-case-summary:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operations must have operationIds\n  unpaywall-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation missing operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # 404 for DOI lookup endpoint\n  unpaywall-doi-not-found:\n    description: DOI lookup must define 404 response\n    message: \"DOI lookup endpoint should define 404 response\"\n    severity: warn\n    given: \"$.paths[/{doi}][get]\"\n    then:\n      field: \"responses.404\"\n      function: truthy\n\n  # API uses GET-only patterns\n  unpaywall-get-only:\n\
  \    description: Unpaywall API is read-only and uses GET requests only\n    message: \"Non-GET method used — Unpaywall API is read-only\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete]\"\n    then:\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unpaywall/refs/heads/main/rules/unpaywall-rules.yml
tags:
- Open Access
- Scholarly Articles
- Research
- Academic
- Libraries
- DOI
- Science
- Spectral
- Linting
- API Governance
---
