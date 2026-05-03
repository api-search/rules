---
api_specs:
- filename: rockwell-factorytalk-optix-openapi.yml
  format: yaml
  label: Rockwell FactoryTalk Optix REST API
  slug: factorytalk-optix-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/openapi/rockwell-factorytalk-optix-openapi.yml
- filename: rockwell-factorytalk-realtime-asyncapi.yml
  format: yaml
  label: Rockwell FactoryTalk Hub API
  slug: factorytalk-hub-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/asyncapi/rockwell-factorytalk-realtime-asyncapi.yml
categories:
- factorytalk
description: Spectral linting rules defining API design standards and conventions for rockwell-factorytalk.
layout: rules
name: rockwell-factorytalk API Rules
provider_name: rockwell-factorytalk
provider_slug: rockwell-factorytalk
rule_count: 10
rules:
- description: All FactoryTalk Optix API operations must define security
  given: $.paths[*][get,post,put,patch,delete]
  name: factorytalk-has-security
  severity: error
- description: All operations must have a unique operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: factorytalk-operation-id-required
  severity: error
- description: FactoryTalk operationIds use camelCase naming
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: factorytalk-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: factorytalk-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: factorytalk-summary-title-case
  severity: warn
- description: Path segments should use lowercase letters, digits, or hyphens
  given: $.paths[*]~
  name: factorytalk-path-kebab-case
  severity: warn
- description: All authenticated endpoints should document 401 Unauthorized
  given: $.paths[*][get,post,put,patch,delete].responses
  name: factorytalk-unauthorized-response
  severity: warn
- description: All component schemas should have descriptions
  given: $.components.schemas[*]
  name: factorytalk-schema-description
  severity: warn
- description: Tag names should use PascalCase for FactoryTalk consistency
  given: $.tags[*].name
  name: factorytalk-tags-pascal-case
  severity: info
- description: List operations should return totalCount for pagination support
  given: $.paths[*][get].responses['200'].content['application/json'].schema
  name: factorytalk-array-total-count
  severity: info
rules_file: rules/rockwell-factorytalk-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/rules/rockwell-factorytalk-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 5
slug: rockwell-factorytalk-rules
source_filename: rockwell-factorytalk-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # FactoryTalk Optix uses OAuth2 and API key authentication\n  factorytalk-has-security:\n    description: All FactoryTalk Optix API operations must define security\n    message: \"Operation must include security (OAuth2 or API key)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # Operations must have operationIds\n  factorytalk-operation-id-required:\n    description: All operations must have a unique operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # OperationIds must use camelCase\n  factorytalk-operation-id-camel-case:\n    description: FactoryTalk operationIds use camelCase naming\n    message: \"OperationId '{{value}}' should be in camelCase format\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries must exist and use Title Case\n  factorytalk-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  factorytalk-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Paths should use lowercase kebab-case\n  factorytalk-path-kebab-case:\n    description: Path segments should use lowercase letters, digits, or hyphens\n    message: \"Path segment should use lowercase kebab-case (no uppercase or underscores)\"\n    severity:\
  \ warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}/.-]+)+$\"\n\n  # Responses must include 401 Unauthorized\n  factorytalk-unauthorized-response:\n    description: All authenticated endpoints should document 401 Unauthorized\n    message: \"Operation should document 401 Unauthorized response for authentication failures\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"401\"]\n\n  # Components must document all schemas\n  factorytalk-schema-description:\n    description: All component schemas should have descriptions\n    message: \"Schema '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Tags must use PascalCase (FactoryTalk convention: Alarms,\
  \ Tags, TrendData, Recipes)\n  factorytalk-tags-pascal-case:\n    description: Tag names should use PascalCase for FactoryTalk consistency\n    message: \"Tag '{{value}}' should use PascalCase\"\n    severity: info\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  # Array responses should include a totalCount field\n  factorytalk-array-total-count:\n    description: List operations should return totalCount for pagination support\n    message: \"Consider including a totalCount field in list response schemas\"\n    severity: info\n    given: \"$.paths[*][get].responses['200'].content['application/json'].schema\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rockwell-factorytalk/refs/heads/main/rules/rockwell-factorytalk-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
