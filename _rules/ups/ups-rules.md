---
api_specs:
- filename: ups-shipping-openapi.yml
  format: yaml
  label: UPS Shipping API
  slug: ups-shipping
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ups/refs/heads/main/openapi/ups-shipping-openapi.yml
categories:
- ups
description: Spectral linting rules defining API design standards and conventions for UPS.
layout: rules
name: UPS API Rules
provider_name: UPS
provider_slug: ups
rule_count: 6
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: ups-operation-ids-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: ups-summaries-title-case
  severity: warn
- description: All non-OAuth operations must use BearerAuth
  given: $.paths[?(!@property.match(/\/oauth\/token/))][get,post,delete]
  name: ups-bearer-auth-required
  severity: warn
- description: UPS API requests use PascalCase wrapper objects
  given: $.paths[*][post,put].requestBody.content.application/json.schema
  name: ups-request-wrappers
  severity: info
- description: Void/cancel operations should use DELETE method
  given: $.paths[?(@property.match(/void|cancel/))]
  name: ups-void-uses-delete
  severity: info
- description: Tracking endpoints use path parameters for tracking numbers
  given: $.paths[?(@property.match(/track/))]
  name: ups-tracking-number-path-param
  severity: info
rules_file: rules/ups-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ups/refs/heads/main/rules/ups-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 3
  warn: 3
slug: ups-rules
source_filename: ups-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ups-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ups-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]* ?)+$\"\n\n  ups-bearer-auth-required:\n    description: All non-OAuth operations must use BearerAuth\n    message: \"Operation must specify BearerAuth security\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/\\\\/oauth\\\\/token/))][get,post,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n     \
  \     type: object\n\n  ups-request-wrappers:\n    description: UPS API requests use PascalCase wrapper objects\n    message: \"UPS request bodies typically use PascalCase wrapper properties\"\n    severity: info\n    given: \"$.paths[*][post,put].requestBody.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  ups-void-uses-delete:\n    description: Void/cancel operations should use DELETE method\n    message: \"Void/cancel operations should use DELETE HTTP method\"\n    severity: info\n    given: \"$.paths[?(@property.match(/void|cancel/))]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [delete]\n\n  ups-tracking-number-path-param:\n    description: Tracking endpoints use path parameters for tracking numbers\n    message: \"Tracking endpoint should use path parameter for inquiry/tracking number\"\n    severity: info\n    given:\
  \ \"$.paths[?(@property.match(/track/))]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{.*\\\\}.*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ups/refs/heads/main/rules/ups-rules.yml
tags:
- Logistics
- Shipping
- Fortune 500
- Supply Chain
- Spectral
- Linting
- API Governance
---
