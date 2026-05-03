---
api_specs:
- filename: vlex-iceberg-anonymization-openapi.yml
  format: yaml
  label: vLex Iceberg Anonymization API
  slug: iceberg-anonymization-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vlex/refs/heads/main/openapi/vlex-iceberg-anonymization-openapi.yml
- filename: vlex-iceberg-legal-research-openapi.yml
  format: yaml
  label: vLex Iceberg Legal Research API
  slug: iceberg-legal-research-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vlex/refs/heads/main/openapi/vlex-iceberg-legal-research-openapi.yml
categories:
- vlex
description: Spectral linting rules defining API design standards and conventions for vLex.
layout: rules
name: vLex API Rules
provider_name: vLex
provider_slug: vlex
rule_count: 8
rules:
- description: Operation IDs must use camelCase to match vLex SDK conventions.
  given: $.paths[*][*].operationId
  name: vlex-operation-ids-camel-case
  severity: warn
- description: All vLex Iceberg API operations require a subscription key.
  given: $.paths[*][*]
  name: vlex-require-subscription-key-security
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: vlex-require-summaries
  severity: error
- description: All operations and schemas must have descriptions.
  given:
  - $.paths[*][*]
  - $.components.schemas[*]
  name: vlex-require-descriptions
  severity: warn
- description: All POST operations must define a requestBody.
  given: $.paths[*].post
  name: vlex-post-operations-have-request-body
  severity: error
- description: All authenticated operations must define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete]
  name: vlex-require-401-response
  severity: warn
- description: Confidence scores must use type number with format float.
  given: $.components.schemas[*].properties[?(@.description && @.description =~ /confidence/i)]
  name: vlex-confidence-fields-use-float
  severity: warn
- description: All vLex Iceberg API paths must be prefixed with /v1/.
  given: $.paths
  name: vlex-v1-api-prefix
  severity: warn
rules_file: rules/vlex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vlex/refs/heads/main/rules/vlex-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: vlex-rules
source_filename: vlex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  vlex-operation-ids-camel-case:\n    description: Operation IDs must use camelCase to match vLex SDK conventions.\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vlex-require-subscription-key-security:\n    description: All vLex Iceberg API operations require a subscription key.\n    message: \"Operation {{path}} must define security\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  vlex-require-summaries:\n    description: All operations must have a summary.\n    message: \"Operation {{path}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  vlex-require-descriptions:\n    description: All operations and schemas must have\
  \ descriptions.\n    message: \"{{path}} must have a description\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  vlex-post-operations-have-request-body:\n    description: All POST operations must define a requestBody.\n    message: \"POST operation {{path}} must define a requestBody\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  vlex-require-401-response:\n    description: All authenticated operations must define a 401 Unauthorized response.\n    message: \"Operation {{path}} must define a 401 response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  vlex-confidence-fields-use-float:\n    description: Confidence scores must use type number with format float.\n    message: \"Confidence field {{path}} must be\
  \ type:number, format:float\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.description && @.description =~ /confidence/i)]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              const: number\n            format:\n              const: float\n\n  vlex-v1-api-prefix:\n    description: All vLex Iceberg API paths must be prefixed with /v1/.\n    message: \"Path {{path}} must start with /v1/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vlex/refs/heads/main/rules/vlex-rules.yml
tags:
- AI
- Classification
- Legal Research
- Legal Tech
- Natural Language Processing
- Privacy
- Spectral
- Linting
- API Governance
---
