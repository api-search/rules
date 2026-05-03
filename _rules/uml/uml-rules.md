---
api_specs:
- filename: plantuml-server-openapi.yml
  format: yaml
  label: PlantUML Server API
  slug: plantuml-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uml/refs/heads/main/openapi/plantuml-server-openapi.yml
- filename: kroki-openapi.yml
  format: yaml
  label: Kroki Diagram API
  slug: kroki
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uml/refs/heads/main/openapi/kroki-openapi.yml
categories:
- uml
description: Spectral linting rules defining API design standards and conventions for UML.
layout: rules
name: UML API Rules
provider_name: UML
provider_slug: uml
rule_count: 8
rules:
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: uml-path-kebab-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: uml-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: uml-operation-summary-title-case
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: uml-tags-required
  severity: warn
- description: Operations must define at least one 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: uml-responses-must-include-success
  severity: error
- description: API info must include contact information
  given: $.info
  name: uml-info-contact-required
  severity: warn
- description: API must define at least one server
  given: $
  name: uml-servers-required
  severity: error
- description: Path parameters must include a description
  given: $.paths[*][*].parameters[?(@.in == "path")]
  name: uml-path-parameters-described
  severity: warn
rules_file: rules/uml-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uml/refs/heads/main/rules/uml-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: uml-rules
source_filename: uml-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  uml-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: Path segment \"{{value}}\" must use kebab-case (lowercase letters, numbers, hyphens only)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(/[a-z0-9{}-]+)+$'\n\n  uml-operation-ids-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: operationId\n      function: truthy\n\n  uml-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$'\n\
  \n  uml-tags-required:\n    description: Operations must have at least one tag\n    message: Operation must include at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  uml-responses-must-include-success:\n    description: Operations must define at least one 2xx success response\n    message: Operation must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  uml-info-contact-required:\n    description: API info must include contact information\n    message: API info must include a contact object\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  uml-servers-required:\n    description: API must define at least one server\n    message: API must include a servers\
  \ array with at least one entry\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  uml-path-parameters-described:\n    description: Path parameters must include a description\n    message: Path parameter \"{{value}}\" must have a description\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.in == \"path\")]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uml/refs/heads/main/rules/uml-rules.yml
tags:
- UML
- Modeling
- Diagrams
- Software Architecture
- Design
- Standards
- Spectral
- Linting
- API Governance
---
