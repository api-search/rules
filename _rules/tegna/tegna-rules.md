---
api_specs:
- filename: tegna-audience-one-openapi.yml
  format: yaml
  label: TEGNA AudienceOne API
  slug: audience-one-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tegna/refs/heads/main/openapi/tegna-audience-one-openapi.yml
- filename: tegna-premion-openapi.yml
  format: yaml
  label: TEGNA Premion OTT Advertising API
  slug: premion-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tegna/refs/heads/main/openapi/tegna-premion-openapi.yml
categories:
- tegna
description: Spectral linting rules defining API design standards and conventions for TEGNA.
layout: rules
name: TEGNA API Rules
provider_name: TEGNA
provider_slug: tegna
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: tegna-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: tegna-operations-have-summaries
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: tegna-title-case-summaries
  severity: warn
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: tegna-operations-have-tags
  severity: warn
- description: All responses must have descriptions.
  given: $.paths[*][*].responses[*]
  name: tegna-responses-have-descriptions
  severity: error
- description: All operations must define security requirements.
  given: $.paths[*][*]
  name: tegna-security-defined
  severity: warn
- description: API must define at least one server.
  given: $
  name: tegna-servers-defined
  severity: error
- description: API must define reusable schemas.
  given: $.components
  name: tegna-components-schemas
  severity: warn
- description: Campaign status fields should use the standard enum values.
  given: $.components.schemas.Campaign.properties.status
  name: tegna-campaign-status-enum
  severity: hint
- description: Date fields should use ISO 8601 format.
  given: $.components.schemas[*].properties[?(@.type === 'string')]
  name: tegna-date-formats
  severity: warn
rules_file: rules/tegna-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tegna/refs/heads/main/rules/tegna-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: tegna-rules
source_filename: tegna-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  tegna-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tegna-operations-have-summaries:\n    description: All operations must have a summary.\n    message: \"Operation must include a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tegna-title-case-summaries:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  tegna-operations-have-tags:\n    description: All operations\
  \ must be tagged.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tegna-responses-have-descriptions:\n    description: All responses must have descriptions.\n    message: \"Response must include a description.\"\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tegna-security-defined:\n    description: All operations must define security requirements.\n    message: \"Operation must include a security definition.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  tegna-servers-defined:\n    description: API must define at least one server.\n    message: \"API must include a servers array.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  tegna-components-schemas:\n    description:\
  \ API must define reusable schemas.\n    message: \"API should define schemas in components/schemas.\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n\n  tegna-campaign-status-enum:\n    description: Campaign status fields should use the standard enum values.\n    message: \"Campaign status should be one of: active, paused, completed, draft.\"\n    severity: hint\n    given: \"$.components.schemas.Campaign.properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  tegna-date-formats:\n    description: Date fields should use ISO 8601 format.\n    message: \"Date field should use format: date or date-time.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.type === 'string')]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tegna/refs/heads/main/rules/tegna-rules.yml
tags:
- Broadcasting
- Media
- Television
- Digital Advertising
- OTT
- CTV
- Fortune 500
- Spectral
- Linting
- API Governance
---
