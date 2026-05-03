---
api_specs:
- filename: truto-admin-openapi.yml
  format: yaml
  label: Truto Admin API
  slug: truto-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/openapi/truto-admin-openapi.yml
- filename: truto-unified-hris-openapi.yml
  format: yaml
  label: Truto Unified HRIS API
  slug: truto-unified-hris-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/openapi/truto-unified-hris-openapi.yml
- filename: truto-unified-ats-openapi.yml
  format: yaml
  label: Truto Unified ATS API
  slug: truto-unified-ats-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/openapi/truto-unified-ats-openapi.yml
- filename: truto-unified-crm-openapi.yml
  format: yaml
  label: Truto Unified CRM API
  slug: truto-unified-crm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/openapi/truto-unified-crm-openapi.yml
categories:
- truto
description: Spectral linting rules defining API design standards and conventions for Truto.
layout: rules
name: Truto API Rules
provider_name: Truto
provider_slug: truto
rule_count: 10
rules:
- description: Truto operation IDs must use camelCase format.
  given: $.paths.*[get,post,put,patch,delete]
  name: truto-operation-ids-camel-case
  severity: warn
- description: All Truto API endpoints must require Bearer token authentication.
  given: $.paths.*[get,post,put,patch,delete]
  name: truto-bearer-auth-security
  severity: error
- description: Truto API paths should not require version prefixes (versioning handled by server URL).
  given: $.paths
  name: truto-versioned-paths
  severity: info
- description: All Truto API operations must have tags for grouping.
  given: $.paths.*[get,post,put,patch,delete]
  name: truto-operations-tagged
  severity: warn
- description: GET operations must include a 200 response with JSON content.
  given: $.paths.*[get].responses.200
  name: truto-response-200-json
  severity: warn
- description: POST creation operations should return 201 status.
  given: $.paths.*[post]
  name: truto-post-201-response
  severity: info
- description: Identifier fields (id, remoteId) must be string type.
  given: $.components.schemas.*.properties[id,remoteId,candidateId,accountId,contactId,opportunityId,employeeId,applicationId,integratedAccountId]
  name: truto-id-string-type
  severity: warn
- description: Date/time fields must use date-time format.
  given: $.components.schemas.*.properties[createdAt,updatedAt,appliedAt,openedAt,closedAt,completedAt,requestedAt]
  name: truto-date-time-format
  severity: warn
- description: List endpoints should support cursor-based pagination.
  given: $.paths.*[get]
  name: truto-pagination-cursor
  severity: info
- description: Unified API list/get endpoints should include integrated_account_id parameter to specify the connected provider instance.
  given: $.paths./unified/*/[get,post]
  name: truto-integrated-account-param
  severity: warn
rules_file: rules/truto-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/rules/truto-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 6
slug: truto-rules
source_filename: truto-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  truto-operation-ids-camel-case:\n    description: Truto operation IDs must use camelCase format.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  truto-bearer-auth-security:\n    description: All Truto API endpoints must require Bearer token authentication.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  truto-versioned-paths:\n    description: Truto API paths should not require version prefixes (versioning handled by server URL).\n    severity: info\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/\"\n\n  truto-operations-tagged:\n    description: All Truto API operations must have tags for grouping.\n    severity: warn\n  \
  \  given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  truto-response-200-json:\n    description: GET operations must include a 200 response with JSON content.\n    severity: warn\n    given: \"$.paths.*[get].responses.200\"\n    then:\n      field: content.application/json\n      function: truthy\n\n  truto-post-201-response:\n    description: POST creation operations should return 201 status.\n    severity: info\n    given: \"$.paths.*[post]\"\n    then:\n      field: responses.201\n      function: truthy\n\n  truto-id-string-type:\n    description: Identifier fields (id, remoteId) must be string type.\n    severity: warn\n    given: \"$.components.schemas.*.properties[id,remoteId,candidateId,accountId,contactId,opportunityId,employeeId,applicationId,integratedAccountId]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  truto-date-time-format:\n    description:\
  \ Date/time fields must use date-time format.\n    severity: warn\n    given: \"$.components.schemas.*.properties[createdAt,updatedAt,appliedAt,openedAt,closedAt,completedAt,requestedAt]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n\n  truto-pagination-cursor:\n    description: List endpoints should support cursor-based pagination.\n    severity: info\n    given: \"$.paths.*[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n\n  truto-integrated-account-param:\n    description: >-\n      Unified API list/get endpoints should include integrated_account_id parameter\n      to specify the connected provider instance.\n    severity: warn\n    given: \"$.paths./unified/*/[get,post]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/truto/refs/heads/main/rules/truto-rules.yml
tags:
- Unified API
- Integration Platform
- HRIS
- ATS
- CRM
- Embedded Integrations
- MCP
- AI Agents
- SaaS
- Spectral
- Linting
- API Governance
---
