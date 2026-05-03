---
api_specs:
- filename: salesforce-net-zero-cloud-rest-api-openapi.yml
  format: yaml
  label: Net Zero Cloud REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-net-zero-cloud/refs/heads/main/openapi/salesforce-net-zero-cloud-rest-api-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Net Zero Cloud.
layout: rules
name: Salesforce Net Zero Cloud API Rules
provider_name: Salesforce Net Zero Cloud
provider_slug: salesforce-net-zero-cloud
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesforce-nzc-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: salesforce-nzc-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: salesforce-nzc-tags-title-case
  severity: warn
- description: Carbon emission records should specify scope
  given: $.components.schemas.CarbonEmissionInput.required
  name: salesforce-nzc-emission-scope-required
  severity: warn
- description: All 200 responses must have a description
  given: $.paths[*][*].responses['200']
  name: salesforce-nzc-response-200-description
  severity: error
- description: API info must include contact details
  given: $.info
  name: salesforce-nzc-contact-required
  severity: error
- description: API must have a version
  given: $.info
  name: salesforce-nzc-version-required
  severity: error
- description: API must define servers
  given: $
  name: salesforce-nzc-servers-required
  severity: error
- description: API must define security requirements
  given: $
  name: salesforce-nzc-security-defined
  severity: error
rules_file: rules/salesforce-net-zero-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-net-zero-cloud/refs/heads/main/rules/salesforce-net-zero-cloud-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: salesforce-net-zero-cloud-rules
source_filename: salesforce-net-zero-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  salesforce-nzc-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-nzc-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  salesforce-nzc-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-nzc-emission-scope-required:\n    description: Carbon emission records should specify scope\n    message: \"\
  Carbon emission input should include Scope field\"\n    severity: warn\n    given: \"$.components.schemas.CarbonEmissionInput.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  salesforce-nzc-response-200-description:\n    description: All 200 responses must have a description\n    severity: error\n    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: description\n      function: truthy\n\n  salesforce-nzc-contact-required:\n    description: API info must include contact details\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salesforce-nzc-version-required:\n    description: API must have a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  salesforce-nzc-servers-required:\n    description: API must define servers\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n\
  \      function: truthy\n\n  salesforce-nzc-security-defined:\n    description: API must define security requirements\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-net-zero-cloud/refs/heads/main/rules/salesforce-net-zero-cloud-rules.yml
tags:
- Carbon Accounting
- Carbon Emissions
- Climate
- Environmental
- ESG
- Net Zero
- Sustainability
- Spectral
- Linting
- API Governance
---
