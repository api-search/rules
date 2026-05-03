---
api_specs:
- filename: cch-tagetik-odata-openapi.yml
  format: yaml
  label: CCH Tagetik OData API
  slug: cch-tagetik-odata-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tagetik/refs/heads/main/openapi/cch-tagetik-odata-openapi.yml
categories:
- tagetik
description: Spectral linting rules defining API design standards and conventions for CCH Tagetik.
layout: rules
name: CCH Tagetik API Rules
provider_name: CCH Tagetik
provider_slug: tagetik
rule_count: 7
rules:
- description: CCH Tagetik OData API must define servers with environment variables
  given: $.servers
  name: tagetik-odata-servers-defined
  severity: error
- description: All OData operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: tagetik-odata-operations-have-descriptions
  severity: warn
- description: OData query parameters ($filter, $select, etc.) should be documented
  given: $.paths[*].get.parameters
  name: tagetik-odata-query-params-documented
  severity: info
- description: Both Basic and OAuth2 authentication must be documented
  given: $.components.securitySchemes
  name: tagetik-auth-both-methods-documented
  severity: warn
- description: OData collection responses must include a value array
  given: $.components.schemas.ODataResponse.properties
  name: tagetik-odata-response-uses-value-array
  severity: warn
- description: All schema components should have descriptions
  given: $.components.schemas[*]
  name: tagetik-schemas-have-descriptions
  severity: warn
- description: Financial amount fields must be numeric type
  given: $.components.schemas[*].properties[Amount,AmountLC]
  name: tagetik-amount-fields-are-numbers
  severity: error
rules_file: rules/cch-tagetik-odata-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tagetik/refs/heads/main/rules/cch-tagetik-odata-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 4
slug: cch-tagetik-odata-rules
source_filename: cch-tagetik-odata-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tagetik-odata-servers-defined:\n    description: CCH Tagetik OData API must define servers with environment variables\n    message: \"API must define at least one server URL\"\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  tagetik-odata-operations-have-descriptions:\n    description: All OData operations should have descriptions\n    message: \"Operation '{{property}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  tagetik-odata-query-params-documented:\n    description: OData query parameters ($filter, $select, etc.) should be documented\n    message: \"OData operations should document standard query parameters\"\n    severity: info\n    given: \"$.paths[*].get.parameters\"\n    then:\n      function: truthy\n\n  tagetik-auth-both-methods-documented:\n\
  \    description: Both Basic and OAuth2 authentication must be documented\n    message: \"API must document both BasicAuth and OAuth2 security schemes\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  tagetik-odata-response-uses-value-array:\n    description: OData collection responses must include a value array\n    message: \"OData response schema should include a 'value' property containing an array\"\n    severity: warn\n    given: \"$.components.schemas.ODataResponse.properties\"\n    then:\n      field: value\n      function: truthy\n\n  tagetik-schemas-have-descriptions:\n    description: All schema components should have descriptions\n    message: \"Schema '{{property}}' is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tagetik-amount-fields-are-numbers:\n    description: Financial amount fields must be numeric type\n  \
  \  message: \"Amount field should be type: number\"\n    severity: error\n    given: \"$.components.schemas[*].properties[Amount,AmountLC]\"\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"^number$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tagetik/refs/heads/main/rules/cch-tagetik-odata-rules.yml
tags:
- Analytics
- Budgeting
- Corporate Performance Management
- ESG
- Financial Close
- Financial Consolidation
- Financial Planning
- OData
- Reporting
- Spectral
- Linting
- API Governance
---
