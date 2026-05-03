---
api_specs:
- filename: zestful-openapi.yml
  format: yaml
  label: Zestful Ingredient Parser API
  slug: zestful
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zestful/refs/heads/main/openapi/zestful-openapi.yml
categories:
- zestful
description: Spectral linting rules defining API design standards and conventions for Zestful.
layout: rules
name: Zestful API Rules
provider_name: Zestful
provider_slug: zestful
rule_count: 7
rules:
- description: Operation IDs must use camelCase (Zestful convention)
  given: $.paths[*][*].operationId
  name: zestful-operation-id-camel-case
  severity: warn
- description: POST endpoints must define a required request body
  given: $.paths[*].post
  name: zestful-request-body-required
  severity: error
- description: Ingredients array must enforce min/maxItems limits
  given: $.paths[*].post.requestBody.content.application/json.schema.properties.ingredients
  name: zestful-ingredients-array-limits
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][*].responses
  name: zestful-response-200-defined
  severity: error
- description: All operations must have tags
  given: $.paths[*][*].tags
  name: zestful-tags-defined
  severity: warn
- description: Operations should define security requirements
  given: $.paths[*][*].security
  name: zestful-security-defined
  severity: warn
- description: API info must include contact details
  given: $.info
  name: zestful-info-contact
  severity: warn
rules_file: rules/zestful-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/zestful/refs/heads/main/rules/zestful-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: zestful-rules
source_filename: zestful-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  zestful-operation-id-camel-case:\n    description: Operation IDs must use camelCase (Zestful convention)\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  zestful-request-body-required:\n    description: POST endpoints must define a required request body\n    message: POST operation must have a required requestBody\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      - field: requestBody\n        function: defined\n      - field: requestBody.required\n        function: truthy\n\n  zestful-ingredients-array-limits:\n    description: Ingredients array must enforce min/maxItems limits\n    message: Ingredients array must define minItems and maxItems\n    severity: warn\n    given: \"$.paths[*].post.requestBody.content.application/json.schema.properties.ingredients\"\
  \n    then:\n      - field: minItems\n        function: defined\n      - field: maxItems\n        function: defined\n\n  zestful-response-200-defined:\n    description: All operations must define a 200 response\n    message: Operation must define a 200 success response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  zestful-tags-defined:\n    description: All operations must have tags\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  zestful-security-defined:\n    description: Operations should define security requirements\n    message: Operation should define security requirements\n    severity: warn\n    given: \"$.paths[*][*].security\"\n    then:\n      function: defined\n\n  zestful-info-contact:\n    description: API info must include contact details\n    message: API info\
  \ must include a contact object\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zestful/refs/heads/main/rules/zestful-rules.yml
tags:
- Food
- Ingredients
- Parsers
- Recipes
- USDA
- Spectral
- Linting
- API Governance
---
