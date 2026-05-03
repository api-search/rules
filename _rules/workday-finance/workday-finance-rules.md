---
api_specs:
- filename: workday-finance-financial-management-openapi.yml
  format: yaml
  label: Workday Financial Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-finance/refs/heads/main/openapi/workday-finance-financial-management-openapi.yml
- filename: workday-finance-procurement-openapi.yml
  format: yaml
  label: Workday Resource Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-finance/refs/heads/main/openapi/workday-finance-procurement-openapi.yml
categories:
- workday
description: Spectral linting rules defining API design standards and conventions for Workday Finance.
layout: rules
name: Workday Finance API Rules
provider_name: Workday Finance
provider_slug: workday-finance
rule_count: 12
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-finance-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-finance-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: workday-finance-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-finance-tags-required
  severity: error
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: workday-finance-path-kebab-case
  severity: warn
- description: GET operations must define a schema for 200 responses.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: workday-finance-response-200-schema
  severity: warn
- description: Bearer authentication must be defined in security schemes.
  given: $.components.securitySchemes
  name: workday-finance-bearer-auth-defined
  severity: error
- description: Collection GET endpoints should support limit and offset parameters.
  given: $.paths[*].get.parameters[*][?(@.name == 'limit')]
  name: workday-finance-pagination-params
  severity: warn
- description: Server URLs must include tenant variable for multi-tenancy.
  given: $.servers[*].url
  name: workday-finance-tenant-in-server-url
  severity: warn
- description: Financial amount fields should use number type for precision.
  given: $.components.schemas[*].properties[?(@property.match(/[Aa]mount|[Bb]alance|[Cc]ost|[Pp]rice/))]
  name: workday-finance-financial-amounts-as-number
  severity: hint
- description: Date fields must specify date or date-time format.
  given: $.components.schemas[*].properties[?(@property.match(/[Dd]ate$|[Oo]n$/))]
  name: workday-finance-date-fields-format
  severity: warn
- description: API info must include contact details.
  given: $.info
  name: workday-finance-info-contact
  severity: warn
rules_file: rules/workday-finance-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-finance/refs/heads/main/rules/workday-finance-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 7
slug: workday-finance-rules
source_filename: workday-finance-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  workday-finance-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  workday-finance-operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  workday-finance-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  workday-finance-tags-required:\n    description: All operations must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n \
  \     function: truthy\n\n  workday-finance-path-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9{}-]+)+$\"\n\n  workday-finance-response-200-schema:\n    description: GET operations must define a schema for 200 responses.\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n\n  workday-finance-bearer-auth-defined:\n    description: Bearer authentication must be defined in security schemes.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  workday-finance-pagination-params:\n    description: Collection GET endpoints should support limit and offset parameters.\n    severity: warn\n    given: \"$.paths[*].get.parameters[*][?(@.name == 'limit')]\"\n    then:\n      field: schema.type\n      function: pattern\n\
  \      functionOptions:\n        match: \"integer\"\n\n  workday-finance-tenant-in-server-url:\n    description: Server URLs must include tenant variable for multi-tenancy.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  workday-finance-financial-amounts-as-number:\n    description: Financial amount fields should use number type for precision.\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@property.match(/[Aa]mount|[Bb]alance|[Cc]ost|[Pp]rice/))]\"\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"number\"\n\n  workday-finance-date-fields-format:\n    description: Date fields must specify date or date-time format.\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@property.match(/[Dd]ate$|[Oo]n$/))]\"\n    then:\n      field: format\n      function: truthy\n\n  workday-finance-info-contact:\n\
  \    description: API info must include contact details.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-finance/refs/heads/main/rules/workday-finance-rules.yml
tags:
- Accounting
- Cloud
- Enterprise
- ERP
- Finance
- Financial Management
- Spectral
- Linting
- API Governance
---
