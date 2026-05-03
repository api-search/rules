---
api_specs:
- filename: openapi.json
  format: json
  label: Workday Extend REST API
  slug: ''
  spec_type: OpenAPI
  url: https://api.workday.com/extend/openapi.json
- filename: workday-extend-orchestration-openapi.yml
  format: yaml
  label: Workday Orchestration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-extend/refs/heads/main/openapi/workday-extend-orchestration-openapi.yml
- filename: workday-extend-custom-objects-openapi.yml
  format: yaml
  label: Workday Custom Objects API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-extend/refs/heads/main/openapi/workday-extend-custom-objects-openapi.yml
- filename: workday-extend-graph-api-openapi.yml
  format: yaml
  label: Workday Graph API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-extend/refs/heads/main/openapi/workday-extend-graph-api-openapi.yml
categories:
- workday
description: Spectral linting rules defining API design standards and conventions for Workday Extend.
layout: rules
name: Workday Extend API Rules
provider_name: Workday Extend
provider_slug: workday-extend
rule_count: 15
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-extend-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-extend-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: workday-extend-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-extend-operation-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-extend-operation-description-required
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: workday-extend-path-kebab-case
  severity: warn
- description: GET operations must define a schema for 200 responses.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: workday-extend-response-200-schema
  severity: warn
- description: All operations must define security requirements.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-extend-security-defined
  severity: error
- description: OAuth2 flows must define scopes.
  given: $.components.securitySchemes[*].flows[*].scopes
  name: workday-extend-oauth2-scopes
  severity: error
- description: All parameters must have a description.
  given: $.components.parameters[*]
  name: workday-extend-parameters-description
  severity: warn
- description: API info must include contact details.
  given: $.info
  name: workday-extend-info-contact
  severity: warn
- description: At least one server must be defined.
  given: $
  name: workday-extend-servers-defined
  severity: error
- description: Schema properties should include descriptions for documentation.
  given: $.components.schemas[*].properties[*]
  name: workday-extend-schema-properties-description
  severity: hint
- description: Collection endpoints should support limit query parameter for pagination.
  given: $.paths[*].get.parameters[*][?(@.name == 'limit')]
  name: workday-extend-pagination-limit-param
  severity: warn
- description: Server URLs must include tenant variable for multi-tenancy.
  given: $.servers[*].url
  name: workday-extend-tenant-variable-required
  severity: warn
rules_file: rules/workday-extend-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-extend/refs/heads/main/rules/workday-extend-rules.yml
severity_counts:
  error: 6
  hint: 1
  info: 0
  warn: 8
slug: workday-extend-rules
source_filename: workday-extend-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  workday-extend-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  workday-extend-operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  workday-extend-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  workday-extend-operation-tags-required:\n    description: All operations must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n\
  \      function: truthy\n\n  workday-extend-operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  workday-extend-path-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  workday-extend-response-200-schema:\n    description: GET operations must define a schema for 200 responses.\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n\n  workday-extend-security-defined:\n    description: All operations must define security requirements.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  workday-extend-oauth2-scopes:\n\
  \    description: OAuth2 flows must define scopes.\n    severity: error\n    given: \"$.components.securitySchemes[*].flows[*].scopes\"\n    then:\n      function: truthy\n\n  workday-extend-parameters-description:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$.components.parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  workday-extend-info-contact:\n    description: API info must include contact details.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  workday-extend-servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  workday-extend-schema-properties-description:\n    description: Schema properties should include descriptions for documentation.\n    severity: hint\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n   \
  \   field: description\n      function: truthy\n\n  workday-extend-pagination-limit-param:\n    description: Collection endpoints should support limit query parameter for pagination.\n    severity: warn\n    given: \"$.paths[*].get.parameters[*][?(@.name == 'limit')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n        match: \"integer\"\n\n  workday-extend-tenant-variable-required:\n    description: Server URLs must include tenant variable for multi-tenancy.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-extend/refs/heads/main/rules/workday-extend-rules.yml
tags:
- Automation
- Custom Applications
- Enterprise
- Extensions
- HCM
- Human Capital Management
- Integration
- Orchestration
- PaaS
- Spectral
- Linting
- API Governance
---
