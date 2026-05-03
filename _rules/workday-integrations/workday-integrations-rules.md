---
api_specs:
- filename: openapi.json
  format: json
  label: Workday REST API
  slug: ''
  spec_type: OpenAPI
  url: https://community.workday.com/sites/default/files/file-hosting/restapi/openapi.json
- filename: workday-integrations-raas-openapi.yml
  format: yaml
  label: Workday RaaS (Report-as-a-Service)
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-integrations/refs/heads/main/openapi/workday-integrations-raas-openapi.yml
- filename: workday-integrations-prism-analytics-openapi.yml
  format: yaml
  label: Workday Prism Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/workday-integrations/refs/heads/main/openapi/workday-integrations-prism-analytics-openapi.yml
categories:
- workday
description: Spectral linting rules defining API design standards and conventions for Workday Integrations.
layout: rules
name: Workday Integrations API Rules
provider_name: Workday Integrations
provider_slug: workday-integrations
rule_count: 11
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-integrations-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-integrations-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: workday-integrations-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-integrations-tags-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: workday-integrations-description-required
  severity: warn
- description: Bearer authentication must be defined.
  given: $.components.securitySchemes
  name: workday-integrations-bearer-auth
  severity: error
- description: Server URLs must include tenant variable.
  given: $.servers[*].url
  name: workday-integrations-tenant-in-url
  severity: warn
- description: Collection endpoints should support limit parameter.
  given: $.paths[*].get.parameters[*][?(@.name == 'limit')]
  name: workday-integrations-pagination-support
  severity: warn
- description: Success responses must define a content schema.
  given: $.paths[*][get,post].responses['200','201'].content.application/json.schema
  name: workday-integrations-response-schema
  severity: warn
- description: Path parameters must have descriptions.
  given: $.paths[*].parameters[?(@.in == 'path')]
  name: workday-integrations-path-params-described
  severity: warn
- description: API info should include external documentation link.
  given: $
  name: workday-integrations-external-docs
  severity: hint
rules_file: rules/workday-integrations-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/workday-integrations/refs/heads/main/rules/workday-integrations-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 6
slug: workday-integrations-rules
source_filename: workday-integrations-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  workday-integrations-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  workday-integrations-operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  workday-integrations-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  workday-integrations-tags-required:\n    description: All operations must have at least one tag.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field:\
  \ tags\n      function: truthy\n\n  workday-integrations-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  workday-integrations-bearer-auth:\n    description: Bearer authentication must be defined.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  workday-integrations-tenant-in-url:\n    description: Server URLs must include tenant variable.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{tenant\\\\}\"\n\n  workday-integrations-pagination-support:\n    description: Collection endpoints should support limit parameter.\n    severity: warn\n    given: \"$.paths[*].get.parameters[*][?(@.name == 'limit')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n\
  \        match: \"integer\"\n\n  workday-integrations-response-schema:\n    description: Success responses must define a content schema.\n    severity: warn\n    given: \"$.paths[*][get,post].responses['200','201'].content.application/json.schema\"\n    then:\n      function: truthy\n\n  workday-integrations-path-params-described:\n    description: Path parameters must have descriptions.\n    severity: warn\n    given: \"$.paths[*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  workday-integrations-external-docs:\n    description: API info should include external documentation link.\n    severity: hint\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/workday-integrations/refs/heads/main/rules/workday-integrations-rules.yml
tags:
- Cloud
- Enterprise Software
- ERP
- Finance
- HCM
- HR
- Integration
- Spectral
- Linting
- API Governance
---
