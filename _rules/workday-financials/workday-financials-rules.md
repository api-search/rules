---
api_specs:
- filename: Financial_Management.json
  format: json
  label: Workday Financial Management API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Financial_Management/v38.2/Financial_Management.json
- filename: Revenue_Management.json
  format: json
  label: Workday Revenue Management API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.2/Revenue_Management.json
- filename: Expenses.json
  format: json
  label: Workday Expenses API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Expenses/v38.2/Expenses.json
- filename: Resource_Management.json
  format: json
  label: Workday Procurement API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Resource_Management/v38.2/Resource_Management.json
- filename: Cash_Management.json
  format: json
  label: Workday Cash Management API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Cash_Management/v38.2/Cash_Management.json
- filename: Financial_Management.json
  format: json
  label: Workday Financial Accounting API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Financial_Management/v38.2/Financial_Management.json
- filename: Report_as_a_Service.json
  format: json
  label: Workday Reporting API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/productionapi/Report_as_a_Service/v38.2/Report_as_a_Service.json
categories:
- workday
description: Spectral linting rules defining API design standards and conventions for Workday Financials.
layout: rules
name: Workday Financials API Rules
provider_name: Workday Financials
provider_slug: workday-financials
rule_count: 12
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-financials-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-financials-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: workday-financials-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-financials-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-financials-description-required
  severity: warn
- description: Bearer authentication must be defined in security schemes.
  given: $.components.securitySchemes
  name: workday-financials-bearer-auth-defined
  severity: error
- description: Server URLs must include tenant variable for multi-tenancy.
  given: $.servers[*].url
  name: workday-financials-tenant-in-server-url
  severity: warn
- description: GET operations must define a schema for 200 responses.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: workday-financials-response-200-schema
  severity: warn
- description: Collection GET operations should support limit parameter.
  given: $.paths[*].get.parameters[*][?(@.name == 'limit')]
  name: workday-financials-pagination-limit
  severity: warn
- description: Amount fields should use number type with double format.
  given: $.components.schemas[*].properties[?(@property.match(/[Aa]mount|[Bb]alance/))]
  name: workday-financials-financial-amounts-number-type
  severity: hint
- description: Date fields should specify date or date-time format.
  given: $.components.schemas[*].properties[?(@property.match(/[Dd]ate$|[Oo]n$/))]
  name: workday-financials-date-format
  severity: warn
- description: API info must include a version.
  given: $.info
  name: workday-financials-info-version
  severity: error
rules_file: rules/workday-financials-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-financials/refs/heads/main/rules/workday-financials-rules.yml
severity_counts:
  error: 5
  hint: 1
  info: 0
  warn: 6
slug: workday-financials-rules
source_filename: workday-financials-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  workday-financials-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  workday-financials-operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  workday-financials-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  workday-financials-tags-required:\n    description: All operations must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field:\
  \ tags\n      function: truthy\n\n  workday-financials-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  workday-financials-bearer-auth-defined:\n    description: Bearer authentication must be defined in security schemes.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  workday-financials-tenant-in-server-url:\n    description: Server URLs must include tenant variable for multi-tenancy.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  workday-financials-response-200-schema:\n    description: GET operations must define a schema for 200 responses.\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n     \
  \ function: truthy\n\n  workday-financials-pagination-limit:\n    description: Collection GET operations should support limit parameter.\n    severity: warn\n    given: \"$.paths[*].get.parameters[*][?(@.name == 'limit')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n        match: \"integer\"\n\n  workday-financials-financial-amounts-number-type:\n    description: Amount fields should use number type with double format.\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@property.match(/[Aa]mount|[Bb]alance/))]\"\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"number\"\n\n  workday-financials-date-format:\n    description: Date fields should specify date or date-time format.\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@property.match(/[Dd]ate$|[Oo]n$/))]\"\n    then:\n      field: format\n      function: truthy\n\n  workday-financials-info-version:\n\
  \    description: API info must include a version.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-financials/refs/heads/main/rules/workday-financials-rules.yml
tags:
- Accounting
- Cloud ERP
- Financial Management
- Procurement
- Spectral
- Linting
- API Governance
---
