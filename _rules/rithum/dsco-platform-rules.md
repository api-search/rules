---
api_specs:
- filename: dsco-platform-openapi.yml
  format: yaml
  label: Dsco Platform API
  slug: dsco-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rithum/refs/heads/main/openapi/dsco-platform-openapi.yml
categories:
- dsco
description: Spectral linting rules defining API design standards and conventions for Rithum.
layout: rules
name: Rithum API Rules
provider_name: Rithum
provider_slug: rithum
rule_count: 11
rules:
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: dsco-operation-has-tag
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: dsco-operation-has-summary
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: dsco-operation-has-description
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: dsco-operation-has-operation-id
  severity: error
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: dsco-operation-id-camel-case
  severity: warn
- description: Error responses should reference a schema
  given: $.paths[*][*].responses[4*,5*].content[*]
  name: dsco-responses-have-error-schema
  severity: warn
- description: POST operations should have a requestBody
  given: $.paths[*].post
  name: dsco-post-has-request-body
  severity: warn
- description: Security scheme should be BearerAuth
  given: $.components.securitySchemes[*]
  name: dsco-bearer-auth-defined
  severity: warn
- description: Batch request schemas should contain array properties
  given: $.components.schemas[*BatchRequest]
  name: dsco-batch-request-has-array
  severity: info
- description: API paths should use kebab-case
  given: $.paths[*]~
  name: dsco-path-uses-kebab-case
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: dsco-schema-has-description
  severity: info
rules_file: rules/dsco-platform-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rithum/refs/heads/main/rules/dsco-platform-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 7
slug: dsco-platform-rules
source_filename: dsco-platform-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Rithum / Dsco API Conventions\n\n  dsco-operation-has-tag:\n    description: All operations must have at least one tag\n    message: Operation {{path}} is missing a tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  dsco-operation-has-summary:\n    description: All operations must have a summary\n    message: Operation {{path}} is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  dsco-operation-has-description:\n    description: All operations should have a description\n    message: Operation {{path}} is missing a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  dsco-operation-has-operation-id:\n    description: All operations must have an operationId\n\
  \    message: Operation {{path}} is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  dsco-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: OperationId {{value}} should use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  dsco-responses-have-error-schema:\n    description: Error responses should reference a schema\n    message: Response {{path}} should define a schema\n    severity: warn\n    given: \"$.paths[*][*].responses[4*,5*].content[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  dsco-post-has-request-body:\n    description: POST operations should have a requestBody\n    message: POST operation {{path}} is missing a requestBody\n    severity: warn\n    given:\
  \ \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  dsco-bearer-auth-defined:\n    description: Security scheme should be BearerAuth\n    message: Security scheme {{path}} should use bearer authentication\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - http\n          required:\n            - type\n\n  dsco-batch-request-has-array:\n    description: Batch request schemas should contain array properties\n    message: Batch request {{path}} should include array fields\n    severity: info\n    given: \"$.components.schemas[*BatchRequest]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  dsco-path-uses-kebab-case:\n    description: API paths should use kebab-case\n    message:\
  \ Path {{path}} should use kebab-case segments\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-z0-9-]*({[a-zA-Z]+})?)*$\"\n\n  dsco-schema-has-description:\n    description: Schema properties should have descriptions\n    message: Schema {{path}} is missing a description\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rithum/refs/heads/main/rules/dsco-platform-rules.yml
tags:
- Commerce
- Dropship
- Marketplace
- Ecommerce
- Supply Chain
- Retail
- Spectral
- Linting
- API Governance
---
