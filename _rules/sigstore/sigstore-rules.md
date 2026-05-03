---
api_specs:
- filename: rekor-openapi.yaml
  format: yaml
  label: Rekor Transparency Log API
  slug: rekor
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sigstore/refs/heads/main/openapi/rekor-openapi.yaml
- filename: fulcio-openapi.json
  format: json
  label: Fulcio Certificate Authority API
  slug: fulcio
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sigstore/refs/heads/main/openapi/fulcio-openapi.json
categories:
- sigstore
description: Spectral linting rules defining API design standards and conventions for Sigstore.
layout: rules
name: Sigstore API Rules
provider_name: Sigstore
provider_slug: sigstore
rule_count: 6
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: sigstore-operation-summary-title-case
  severity: warn
- description: All API paths must include a version prefix.
  given: $.paths[*]~
  name: sigstore-api-versioned-paths
  severity: warn
- description: Operations must include at least one tag.
  given: $.paths[*][*]
  name: sigstore-tags-defined
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][*]
  name: sigstore-operationid-required
  severity: error
- description: API operations should document error responses.
  given: $.paths[*][*].responses
  name: sigstore-error-response
  severity: warn
- description: API info and operations must have descriptions.
  given:
  - $.info
  - $.paths[*][*]
  name: sigstore-description-required
  severity: warn
rules_file: rules/sigstore-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sigstore/refs/heads/main/rules/sigstore-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 5
slug: sigstore-rules
source_filename: sigstore-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  sigstore-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  sigstore-api-versioned-paths:\n    description: All API paths must include a version prefix.\n    message: \"Path '{{property}}' should include a version segment (e.g., /api/v1/ or /api/v2/).\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+\"\n\n  sigstore-tags-defined:\n    description: Operations must include at least one tag.\n    message: \"Operation is missing tags.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  sigstore-operationid-required:\n\
  \    description: Every operation must have an operationId.\n    message: \"Operation is missing an operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sigstore-error-response:\n    description: API operations should document error responses.\n    message: \"Operation should document at least one error response (4xx/5xx).\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 2\n\n  sigstore-description-required:\n    description: API info and operations must have descriptions.\n    message: \"{{property}} is missing a description.\"\n    severity: warn\n    given:\n      - \"$.info\"\n      - \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sigstore/refs/heads/main/rules/sigstore-rules.yml
tags:
- Certificate Authority
- Code Signing
- Containers
- Cryptography
- Open Source
- PKI
- Security
- Software Supply Chain
- Transparency Log
- Spectral
- Linting
- API Governance
---
