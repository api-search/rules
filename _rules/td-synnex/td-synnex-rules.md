---
api_specs:
- filename: td-synnex-streamone-ion-openapi.yml
  format: yaml
  label: TD SYNNEX StreamOne Ion API
  slug: streamone-ion
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/td-synnex/refs/heads/main/openapi/td-synnex-streamone-ion-openapi.yml
categories:
- tdsynnex
description: Spectral linting rules defining API design standards and conventions for TD SYNNEX.
layout: rules
name: TD SYNNEX API Rules
provider_name: TD SYNNEX
provider_slug: td-synnex
rule_count: 12
rules:
- description: All API paths should be versioned with /v3/ prefix
  given: $.paths[*]~
  name: tdsynnex-path-versioning
  severity: warn
- description: Partner resource paths should include {accountId} parameter
  given: $.paths[/v3/*]~
  name: tdsynnex-path-account-id
  severity: warn
- description: All operations must have operationId defined
  given: $.paths[*][get,post,put,delete,patch]
  name: tdsynnex-operation-ids-required
  severity: error
- description: operationId values should use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: tdsynnex-operation-ids-camelcase
  severity: warn
- description: All operations should be tagged
  given: $.paths[*][get,post,put,delete,patch]
  name: tdsynnex-tags-defined
  severity: warn
- description: Operations (except token endpoint) should require OAuth2
  given: $.paths[/v3/*][get,post,put,delete,patch]
  name: tdsynnex-security-defined
  severity: warn
- description: GET operations should define a 200 success response
  given: $.paths[*].get.responses
  name: tdsynnex-responses-success
  severity: error
- description: POST create operations should return 201 Created
  given: $.paths[/v3/accounts/{accountId}/customers,/v3/accounts/{accountId}/orders,/v3/accounts/{accountId}/customers/{customerId}/carts].post.responses
  name: tdsynnex-post-responses-201
  severity: warn
- description: Authenticated operations should define 401 Unauthorized
  given: $.paths[/v3/*][get,post,put,delete,patch].responses
  name: tdsynnex-error-401
  severity: warn
- description: Operation summaries should use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: tdsynnex-summary-title-case
  severity: warn
- description: POST and PUT operations should specify application/json content type
  given: $.paths[*][post,put].requestBody.content
  name: tdsynnex-request-body-content-type
  severity: warn
- description: List operations should support pagination parameters
  given: $.paths[*].get
  name: tdsynnex-pagination-parameters
  severity: info
rules_file: rules/td-synnex-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/td-synnex/refs/heads/main/rules/td-synnex-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 9
slug: td-synnex-rules
source_filename: td-synnex-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tdsynnex-path-versioning:\n    description: All API paths should be versioned with /v3/ prefix\n    message: \"Path '{{property}}' should be versioned with /v3/ prefix (or /oauth/ for auth)\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v3/|/oauth/)\"\n\n  tdsynnex-path-account-id:\n    description: Partner resource paths should include {accountId} parameter\n    message: \"Partner resource path '{{property}}' should include {accountId}\"\n    severity: warn\n    given: \"$.paths[/v3/*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{accountId\\\\}.*\"\n\n  tdsynnex-operation-ids-required:\n    description: All operations must have operationId defined\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function:\
  \ defined\n\n  tdsynnex-operation-ids-camelcase:\n    description: operationId values should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tdsynnex-tags-defined:\n    description: All operations should be tagged\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: defined\n\n  tdsynnex-security-defined:\n    description: Operations (except token endpoint) should require OAuth2\n    message: \"Operation should define security requirements\"\n    severity: warn\n    given: \"$.paths[/v3/*][get,post,put,delete,patch]\"\n    then:\n      function: defined\n\n  tdsynnex-responses-success:\n    description: GET operations should define a 200 success response\n   \
  \ message: \"GET operation is missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  tdsynnex-post-responses-201:\n    description: POST create operations should return 201 Created\n    message: \"POST create operation should return 201\"\n    severity: warn\n    given: \"$.paths[/v3/accounts/{accountId}/customers,/v3/accounts/{accountId}/orders,/v3/accounts/{accountId}/customers/{customerId}/carts].post.responses\"\n    then:\n      field: \"201\"\n      function: defined\n\n  tdsynnex-error-401:\n    description: Authenticated operations should define 401 Unauthorized\n    message: \"Operation is missing 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[/v3/*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  tdsynnex-summary-title-case:\n    description: Operation summaries should use Title Case\n    message: \"Summary '{{value}}'\
  \ should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  tdsynnex-request-body-content-type:\n    description: POST and PUT operations should specify application/json content type\n    message: \"POST/PUT operation should specify application/json request body content type\"\n    severity: warn\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      field: \"application/json\"\n      function: defined\n\n  tdsynnex-pagination-parameters:\n    description: List operations should support pagination parameters\n    message: \"List operation should support page and pageSize parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/td-synnex/refs/heads/main/rules/td-synnex-rules.yml
tags:
- Technology Distribution
- IT Distribution
- Cloud
- Reseller
- StreamOne
- Fortune 100
- B2B
- Spectral
- Linting
- API Governance
---
