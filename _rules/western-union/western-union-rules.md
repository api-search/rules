---
api_specs:
- filename: western-union-mass-payments-openapi.yml
  format: yaml
  label: Western Union Mass Payments API
  slug: mass-payments
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/western-union/refs/heads/main/openapi/western-union-mass-payments-openapi.yml
categories:
- wu
description: Spectral linting rules defining API design standards and conventions for western-union.
layout: rules
name: western-union API Rules
provider_name: western-union
provider_slug: western-union
rule_count: 8
rules:
- description: Operation IDs must use camelCase.
  given: $.paths.*.*.operationId
  name: wu-operation-id-camel-case
  severity: warn
- description: All customer-specific paths must include the {clientId} path parameter to scope operations to a specific WU partner account.
  given: $.paths[?(@.startsWith('/customers'))][*]~
  name: wu-client-id-in-path
  severity: warn
- description: Successful responses must return application/json.
  given: $.paths.*.*.responses.200.content
  name: wu-response-200-content-type
  severity: warn
- description: Each operation must include at least one tag.
  given: $.paths.*.*.tags
  name: wu-tags-defined
  severity: warn
- description: Each operation must have a description.
  given: $.paths.*.*.description
  name: wu-description-required
  severity: warn
- description: API paths must not have trailing slashes.
  given: $.paths[*]~
  name: wu-no-trailing-slash
  severity: error
- description: Payment amount fields should be described as minor units (e.g., cents) in their schema description.
  given: $.components.schemas.PaymentRequest.properties.amount.description
  name: wu-amount-in-minor-units
  severity: info
- description: All operations must use mutualTLS authentication.
  given: $.paths.*.*.security
  name: wu-mtls-security
  severity: warn
rules_file: rules/western-union-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/western-union/refs/heads/main/rules/western-union-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 6
slug: western-union-rules
source_filename: western-union-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  wu-operation-id-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  wu-client-id-in-path:\n    description: >-\n      All customer-specific paths must include the {clientId} path parameter\n      to scope operations to a specific WU partner account.\n    message: \"Path '{{path}}' should include '{clientId}' for scoping to partner account.\"\n    severity: warn\n    given: \"$.paths[?(@.startsWith('/customers'))][*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/\\\\{clientId\\\\}/\"\n\n  wu-response-200-content-type:\n    description: Successful responses must return application/json.\n    message: \"Response at '{{path}}' should define application/json content.\"\n  \
  \  severity: warn\n    given: \"$.paths.*.*.responses.200.content\"\n    then:\n      function: truthy\n\n  wu-tags-defined:\n    description: Each operation must include at least one tag.\n    message: \"Operation at '{{path}}' must include at least one tag.\"\n    severity: warn\n    given: \"$.paths.*.*.tags\"\n    then:\n      function: truthy\n\n  wu-description-required:\n    description: Each operation must have a description.\n    message: \"Operation at '{{path}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths.*.*.description\"\n    then:\n      function: truthy\n\n  wu-no-trailing-slash:\n    description: API paths must not have trailing slashes.\n    message: \"Path '{{value}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  wu-amount-in-minor-units:\n    description: >-\n      Payment amount fields should be described as minor\
  \ units (e.g., cents)\n      in their schema description.\n    message: \"Amount field should describe minor unit format.\"\n    severity: info\n    given: \"$.components.schemas.PaymentRequest.properties.amount.description\"\n    then:\n      function: truthy\n\n  wu-mtls-security:\n    description: All operations must use mutualTLS authentication.\n    message: \"Operation at '{{path}}' must declare mtlsAuth security.\"\n    severity: warn\n    given: \"$.paths.*.*.security\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/western-union/refs/heads/main/rules/western-union-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
