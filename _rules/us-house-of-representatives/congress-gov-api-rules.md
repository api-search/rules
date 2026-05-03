---
api_specs:
- filename: congress-gov-api-openapi.yml
  format: yaml
  label: Congress.gov API
  slug: congress-gov-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-house-of-representatives/refs/heads/main/openapi/congress-gov-api-openapi.yml
categories:
- congress
description: Spectral linting rules defining API design standards and conventions for US House of Representatives.
layout: rules
name: US House of Representatives API Rules
provider_name: US House of Representatives
provider_slug: us-house-of-representatives
rule_count: 11
rules:
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: congress-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: congress-operations-have-summaries
  severity: error
- description: All operations should be tagged for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: congress-operations-have-tags
  severity: warn
- description: All GET operations should define a 200 response
  given: $.paths[*][get]
  name: congress-response-200-defined
  severity: warn
- description: All paths should use the v3 versioning format
  given: $.servers[*].url
  name: congress-v3-path-prefix
  severity: info
- description: Format parameters should list valid values
  given: $.paths[*][*].parameters[?(@.name == 'format')]
  name: congress-format-param-documented
  severity: info
- description: Limit parameters should specify the maximum allowed value
  given: $.paths[*][*].parameters[?(@.name == 'limit')]
  name: congress-limit-param-max
  severity: info
- description: API should define authentication/security scheme
  given: $.components.securitySchemes
  name: congress-security-scheme-defined
  severity: warn
- description: API should include contact information
  given: $.info
  name: congress-info-contact-present
  severity: warn
- description: Tags must use Title Case naming
  given: $.tags[*].name
  name: congress-tags-title-case
  severity: warn
- description: API paths should not hardcode version numbers
  given: $.paths
  name: congress-path-versioned
  severity: info
rules_file: rules/congress-gov-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-house-of-representatives/refs/heads/main/rules/congress-gov-api-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 4
  warn: 6
slug: congress-gov-api-rules
source_filename: congress-gov-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  congress-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: Operation ID \"{{value}}\" should use camelCase (e.g., listBills, getMember)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  congress-operations-have-summaries:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  congress-operations-have-tags:\n    description: All operations should be tagged for grouping\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  congress-response-200-defined:\n    description: All GET operations\
  \ should define a 200 response\n    message: GET operation is missing a 200 OK response\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  congress-v3-path-prefix:\n    description: All paths should use the v3 versioning format\n    message: API paths should reflect versioning\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\/v[0-9]+$\"\n\n  congress-format-param-documented:\n    description: Format parameters should list valid values\n    message: Format parameter should specify valid options\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'format')]\"\n    then:\n      field: schema.enum\n      function: truthy\n\n  congress-limit-param-max:\n    description: Limit parameters should specify the maximum allowed value\n    message: Limit parameter should specify maximum value (250)\n    severity: info\n    given:\
  \ \"$.paths[*][*].parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema.maximum\n      function: truthy\n\n  congress-security-scheme-defined:\n    description: API should define authentication/security scheme\n    message: API specification should define security schemes\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  congress-info-contact-present:\n    description: API should include contact information\n    message: API info is missing contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  congress-tags-title-case:\n    description: Tags must use Title Case naming\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n\n  congress-path-versioned:\n    description: API paths should not hardcode version\
  \ numbers\n    message: Version should be in server URL, not paths\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^\\/v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-house-of-representatives/refs/heads/main/rules/congress-gov-api-rules.yml
tags:
- Federal Government
- Legislation
- Congress
- Legislative Data
- Bills
- Members
- Committees
- Spectral
- Linting
- API Governance
---
