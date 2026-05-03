---
api_specs:
- filename: routeros-rest-api-openapi.yml
  format: yaml
  label: RouterOS REST API
  slug: routeros-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/routeros/refs/heads/main/openapi/routeros-rest-api-openapi.yml
categories:
- routeros
description: Spectral linting rules defining API design standards and conventions for RouterOS.
layout: rules
name: RouterOS API Rules
provider_name: RouterOS
provider_slug: routeros
rule_count: 10
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: routeros-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase (RouterOS convention).
  given: $.paths[*][*].operationId
  name: routeros-operationid-kebab-case
  severity: warn
- description: API paths must use kebab-case segments mirroring RouterOS menu hierarchy.
  given: $.paths[*]~
  name: routeros-path-kebab-case
  severity: warn
- description: All tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: routeros-tags-title-case
  severity: warn
- description: GET operations must return a schema in 200 responses.
  given: $.paths[*].get.responses['200'].content[*].schema
  name: routeros-response-200-schema
  severity: warn
- description: RouterOS REST API uses HTTP Basic Auth; security must be defined.
  given: $.paths[*][*]
  name: routeros-security-basic-auth
  severity: warn
- description: Error responses must reference the Error schema component.
  given: $.paths[*][*].responses['4XX','5XX'].content[*].schema
  name: routeros-error-schema-defined
  severity: hint
- description: RouterOS uses PUT (not POST) for creating resources.
  given: $.paths[*].post
  name: routeros-put-for-create
  severity: info
- description: RouterOS IDs use asterisk-prefixed strings (e.g., *1). Document this in examples.
  given: $.paths[*][*].parameters[?(@.name == 'id')].example
  name: routeros-id-path-param-star-prefix
  severity: hint
- description: RouterOS returns all values as strings even for numeric/boolean properties.
  given: $.components.schemas[*].properties[?(@.type == 'boolean')]
  name: routeros-string-typed-values
  severity: info
rules_file: rules/routeros-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/routeros/refs/heads/main/rules/routeros-rules.yml
severity_counts:
  error: 0
  hint: 2
  info: 2
  warn: 6
slug: routeros-rules
source_filename: routeros-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  routeros-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*(\\\\s[A-Z][a-z0-9]*)*)(\\\\s[A-Z][a-z]*)*$\"\n\n  routeros-operationid-kebab-case:\n    description: operationId must use camelCase (RouterOS convention).\n    message: \"operationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  routeros-path-kebab-case:\n    description: API paths must use kebab-case segments mirroring RouterOS menu hierarchy.\n    message: \"Path segment '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(\\\\{[a-zA-Z][a-zA-Z0-9-]*\\\\})?)*$\"\n\n  routeros-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9\\\\s]*$\"\n\n  routeros-response-200-schema:\n    description: GET operations must return a schema in 200 responses.\n    message: \"GET operation '{{path}}' must define a schema for the 200 response.\"\n    severity: warn\n    given: \"$.paths[*].get.responses['200'].content[*].schema\"\n    then:\n      function: truthy\n\n  routeros-security-basic-auth:\n    description: RouterOS REST API uses HTTP Basic Auth; security must be defined.\n    message: \"Operation must reference a security scheme (RouterOS uses basicAuth).\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: truthy\n\
  \      field: security\n      severity: hint\n\n  routeros-error-schema-defined:\n    description: Error responses must reference the Error schema component.\n    message: \"Error response should reference the Error schema.\"\n    severity: hint\n    given: \"$.paths[*][*].responses['4XX','5XX'].content[*].schema\"\n    then:\n      function: truthy\n\n  routeros-put-for-create:\n    description: RouterOS uses PUT (not POST) for creating resources.\n    message: \"Use PUT for creating RouterOS resources; POST is reserved for console commands.\"\n    severity: info\n    given: \"$.paths[*].post\"\n    then:\n      function: falsy\n      severity: hint\n\n  routeros-id-path-param-star-prefix:\n    description: RouterOS IDs use asterisk-prefixed strings (e.g., *1). Document this in examples.\n    message: \"Path parameter 'id' should document the RouterOS *N ID format.\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.name == 'id')].example\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^\\\\*[0-9]+$\"\n\n  routeros-string-typed-values:\n    description: RouterOS returns all values as strings even for numeric/boolean properties.\n    message: \"RouterOS API returns all values as strings. Document boolean-like fields with enum ['true','false'].\"\n    severity: info\n    given: \"$.components.schemas[*].properties[?(@.type == 'boolean')]\"\n    then:\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/routeros/refs/heads/main/rules/routeros-rules.yml
tags:
- Networking
- Routers
- Network Management
- Firewall
- MikroTik
- Spectral
- Linting
- API Governance
---
