---
categories:
- w3c
description: Spectral linting rules defining API design standards and conventions for W3C.
layout: rules
name: W3C API Rules
provider_name: W3C
provider_slug: w3c
rule_count: 7
rules:
- description: W3C API definitions should include contact information.
  given: $.info
  name: w3c-api-info-contact
  severity: info
- description: Operation summaries should use Title Case.
  given: $.paths[*][*].summary
  name: w3c-api-operation-summary-title-case
  severity: warn
- description: All operations should have a description for documentation quality.
  given: $.paths[*][*]
  name: w3c-api-has-description
  severity: info
- description: Every operation should define at least one response.
  given: $.paths[*][*].responses
  name: w3c-api-response-defined
  severity: warn
- description: GET operations should have a 200 response defined.
  given: $.paths[*].get.responses
  name: w3c-api-200-response
  severity: warn
- description: W3C API paths should be versioned.
  given: $.servers[*].url
  name: w3c-api-path-versioned
  severity: info
- description: Operations should be tagged for logical grouping.
  given: $.paths[*][*]
  name: w3c-api-tags-defined
  severity: info
rules_file: rules/w3c-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/w3c/refs/heads/main/rules/w3c-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 4
  warn: 3
slug: w3c-rules
source_filename: w3c-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # W3C API-specific rules for the W3C API (api.w3.org)\n  w3c-api-info-contact:\n    description: W3C API definitions should include contact information.\n    severity: info\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  w3c-api-operation-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  w3c-api-has-description:\n    description: All operations should have a description for documentation quality.\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  w3c-api-response-defined:\n    description: Every operation should define at least one response.\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n \
  \   then:\n      function: truthy\n\n  w3c-api-200-response:\n    description: GET operations should have a 200 response defined.\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  w3c-api-path-versioned:\n    description: W3C API paths should be versioned.\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/[v][0-9]\"\n\n  w3c-api-tags-defined:\n    description: Operations should be tagged for logical grouping.\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/w3c/refs/heads/main/rules/w3c-rules.yml
tags:
- Accessibility
- Standards
- Web
- Web Standards
- Spectral
- Linting
- API Governance
---
