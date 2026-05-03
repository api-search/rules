---
api_specs:
- filename: ssl-tls-certificate-management-openapi.yml
  format: yaml
  label: Let's Encrypt ACME API
  slug: lets-encrypt-acme
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ssl-tls/refs/heads/main/openapi/ssl-tls-certificate-management-openapi.yml
categories:
- ssl
description: Spectral linting rules defining API design standards and conventions for SSL/TLS.
layout: rules
name: SSL/TLS API Rules
provider_name: SSL/TLS
provider_slug: ssl-tls
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ssl-tls-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: ssl-tls-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: ssl-tls-tags-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][*].description
  name: ssl-tls-description-required
  severity: warn
- description: Certificate management operations must require authentication
  given: $.paths[*/certificates*][post,delete]
  name: ssl-tls-certificates-require-auth
  severity: error
- description: Date fields in schemas should use date-time format
  given: $.components.schemas[*].properties[?(@.name =~ /(At|Before|After|Date|Expiry)$/)]
  name: ssl-tls-date-fields-format
  severity: warn
- description: All operations must define at least one success response
  given: $.paths[*][*].responses
  name: ssl-tls-response-success-defined
  severity: error
rules_file: rules/ssl-tls-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ssl-tls/refs/heads/main/rules/ssl-tls-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: ssl-tls-rules
source_filename: ssl-tls-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ssl-tls-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s?)+$\"\n\n  ssl-tls-operationid-camel-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ssl-tls-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  ssl-tls-description-required:\n    description: All operations must have a description\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  ssl-tls-certificates-require-auth:\n    description: Certificate\
  \ management operations must require authentication\n    severity: error\n    given: \"$.paths[*/certificates*][post,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  ssl-tls-date-fields-format:\n    description: Date fields in schemas should use date-time format\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.name =~ /(At|Before|After|Date|Expiry)$/)]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n          - date-time\n\n  ssl-tls-response-success-defined:\n    description: All operations must define at least one success response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ssl-tls/refs/heads/main/rules/ssl-tls-rules.yml
tags:
- SSL/TLS
- TLS
- Certificates
- PKI
- Cryptography
- Certificate Authority
- HTTPS
- Spectral
- Linting
- API Governance
---
