---
api_specs:
- filename: searchstax-provisioning-openapi.yml
  format: yaml
  label: SearchStax Provisioning API
  slug: searchstax-provisioning-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/searchstax/refs/heads/main/openapi/searchstax-provisioning-openapi.yml
categories:
- searchstax
description: Spectral linting rules defining API design standards and conventions for SearchStax.
layout: rules
name: SearchStax API Rules
provider_name: SearchStax
provider_slug: searchstax
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: searchstax-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: searchstax-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: searchstax-summaries-title-case
  severity: warn
- description: Deployment management paths must include account_name path parameter
  given: $.paths['/api/rest/v2/account/{account_name}/*']
  name: searchstax-account-path-parameter
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*][delete].responses
  name: searchstax-delete-responses
  severity: warn
- description: POST create operations should return 201 Created
  given: $.paths[*][post].responses
  name: searchstax-post-response-201
  severity: info
- description: Operations should document authentication requirements
  given: $.paths[*][*]
  name: searchstax-token-auth
  severity: error
- description: Path parameters should use snake_case
  given: $.paths[*][*].parameters[?(@.in=='path')].name
  name: searchstax-path-parameters-kebab
  severity: info
rules_file: rules/searchstax-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/searchstax/refs/heads/main/rules/searchstax-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: searchstax-rules
source_filename: searchstax-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  searchstax-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  searchstax-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  searchstax-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  searchstax-account-path-parameter:\n    description: Deployment management paths must include account_name path parameter\n    severity: warn\n    given: \"$.paths['/api/rest/v2/account/{account_name}/*']\"\n    then:\n     \
  \ function: truthy\n\n  searchstax-delete-responses:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*][delete].responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  searchstax-post-response-201:\n    description: POST create operations should return 201 Created\n    severity: info\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  searchstax-token-auth:\n    description: Operations should document authentication requirements\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  searchstax-path-parameters-kebab:\n    description: Path parameters should use snake_case\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in=='path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/searchstax/refs/heads/main/rules/searchstax-rules.yml
tags:
- Search
- Solr
- Managed Search
- Search Infrastructure
- Full-Text Search
- Site Search
- Spectral
- Linting
- API Governance
---
