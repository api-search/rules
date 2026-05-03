---
api_specs:
- filename: synnex-streamone-ion-openapi.yml
  format: yaml
  label: TD SYNNEX StreamOne ION API
  slug: streamone-ion
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synnex/refs/heads/main/openapi/synnex-streamone-ion-openapi.yml
categories:
- account
- list
- oauth
- operation
- path
- paths
- response
description: Spectral linting rules defining API design standards and conventions for Synnex.
layout: rules
name: Synnex API Rules
provider_name: Synnex
provider_slug: synnex
rule_count: 11
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description
  severity: warn
- description: All path parameters must have a description.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: path-param-documented
  severity: error
- description: Resource endpoints should include accountId path parameter.
  given: $.paths['/accounts/{accountId}/*']
  name: account-id-required
  severity: info
- description: List operations (GET returning arrays) should support pagination parameters.
  given: $.paths[*].get.parameters
  name: list-pagination
  severity: warn
- description: All operations must use OAuth 2.0 bearer token authentication.
  given: $.components.securitySchemes
  name: oauth-security
  severity: error
- description: Successful responses must include a response body schema.
  given: $.paths[*][*].responses['200','201'].content['application/json']
  name: response-body-schema
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths
  name: paths-kebab-case
  severity: warn
rules_file: rules/synnex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/synnex/refs/heads/main/rules/synnex-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 6
slug: synnex-rules
source_filename: synnex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Require operationId on all operations\n  operation-operationId:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Require summary on all operations\n  operation-summary:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Enforce Title Case on operation summaries\n  operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Require tags on all operations\n  operation-tags:\n    description: All operations must have at least one tag.\n \
  \   severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Require description\n  operation-description:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  # Path parameters must be documented\n  path-param-documented:\n    description: All path parameters must have a description.\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  # Account ID path parameter must exist for resource endpoints\n  account-id-required:\n    description: Resource endpoints should include accountId path parameter.\n    severity: info\n    given: \"$.paths['/accounts/{accountId}/*']\"\n    then:\n      function: truthy\n\n  # Require pagination on list operations\n  list-pagination:\n    description:\
  \ List operations (GET returning arrays) should support pagination parameters.\n    severity: warn\n    given: \"$.paths[*].get.parameters\"\n    then:\n      function: truthy\n\n  # OAuth2 bearer auth required\n  oauth-security:\n    description: All operations must use OAuth 2.0 bearer token authentication.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  # Response body for 2xx must have schema\n  response-body-schema:\n    description: Successful responses must include a response body schema.\n    severity: warn\n    given: \"$.paths[*][*].responses['200','201'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  # Paths must use kebab-case\n  paths-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/synnex/refs/heads/main/rules/synnex-rules.yml
tags:
- Technology Distribution
- IT Distribution
- Cloud Marketplace
- Fortune 100
- Supply Chain
- Spectral
- Linting
- API Governance
---
