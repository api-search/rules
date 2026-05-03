---
api_specs:
- filename: whatfix-openapi.yml
  format: yaml
  label: Whatfix API
  slug: whatfix-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/whatfix/refs/heads/main/openapi/whatfix-openapi.yml
categories:
- whatfix
description: Spectral linting rules defining API design standards and conventions for Whatfix.
layout: rules
name: Whatfix API Rules
provider_name: Whatfix
provider_slug: whatfix
rule_count: 10
rules:
- description: All Whatfix API paths must include {accountId} as the first path segment.
  given: $.paths.*~
  name: whatfix-account-id-in-path
  severity: error
- description: All operationIds should use camelCase.
  given: $.paths.*.*.operationId
  name: whatfix-operation-ids-camel-case
  severity: warn
- description: Analytics endpoints should have startDate and endDate parameters.
  given: $.paths[?(@property.includes('analytics'))].get
  name: whatfix-analytics-date-params
  severity: warn
- description: All operations must reference the ApiKeyAuth security scheme.
  given: $.paths.*.*
  name: whatfix-security-required
  severity: error
- description: All GET operations must define a 200 response.
  given: $.paths.*.get
  name: whatfix-response-200-defined
  severity: error
- description: List endpoints (returning arrays) should include pagination in response schema.
  given: $.paths.*.get.responses.200.content.application/json.schema
  name: whatfix-pagination-on-list-endpoints
  severity: warn
- description: All operations should define 401 and 403 error responses.
  given: $.paths.*.*
  name: whatfix-error-responses-defined
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths.*.*
  name: whatfix-tags-on-operations
  severity: error
- description: Path segments (excluding parameters) should use kebab-case.
  given: $.paths.*~
  name: whatfix-kebab-case-paths
  severity: warn
- description: All operations should have a description.
  given: $.paths.*.*
  name: whatfix-description-on-operations
  severity: warn
rules_file: rules/whatfix-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/whatfix/refs/heads/main/rules/whatfix-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: whatfix-rules
source_filename: whatfix-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  whatfix-account-id-in-path:\n    description: All Whatfix API paths must include {accountId} as the first path segment.\n    message: Path '{{path}}' must start with /{accountId}.\n    severity: error\n    given: \"$.paths.*~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/\\\\{accountId\\\\}\"\n\n  whatfix-operation-ids-camel-case:\n    description: All operationIds should use camelCase.\n    message: OperationId '{{value}}' should use camelCase.\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  whatfix-analytics-date-params:\n    description: Analytics endpoints should have startDate and endDate parameters.\n    message: Analytics endpoint '{{path}}' should document startDate and endDate query parameters.\n    severity: warn\n    given: \"$.paths[?(@property.includes('analytics'))].get\"\n \
  \   then:\n      field: parameters\n      function: truthy\n\n  whatfix-security-required:\n    description: All operations must reference the ApiKeyAuth security scheme.\n    message: Operation '{{path}}' is missing ApiKeyAuth security requirement.\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  whatfix-response-200-defined:\n    description: All GET operations must define a 200 response.\n    message: GET operation '{{path}}' must define a 200 response.\n    severity: error\n    given: \"$.paths.*.get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  whatfix-pagination-on-list-endpoints:\n    description: List endpoints (returning arrays) should include pagination in response schema.\n    message: List endpoint '{{path}}' response should include pagination object.\n \
  \   severity: warn\n    given: \"$.paths.*.get.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            pagination:\n              type: object\n\n  whatfix-error-responses-defined:\n    description: All operations should define 401 and 403 error responses.\n    message: Operation '{{path}}' should define 401 and 403 responses.\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - '401'\n            - '403'\n\n  whatfix-tags-on-operations:\n    description: All operations must have at least one tag.\n    message: Operation '{{path}}' must have at least one tag.\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  whatfix-kebab-case-paths:\n    description: Path segments (excluding parameters) should use\
  \ kebab-case.\n    message: Path segment in '{{path}}' should use kebab-case.\n    severity: warn\n    given: \"$.paths.*~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/\\\\{[a-zA-Z]+\\\\}|/[a-z0-9-]+)*$\"\n\n  whatfix-description-on-operations:\n    description: All operations should have a description.\n    message: Operation '{{path}}' is missing a description.\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/whatfix/refs/heads/main/rules/whatfix-rules.yml
tags:
- Digital Adoption
- SaaS Management
- User Onboarding
- In-App Guidance
- Analytics
- Change Management
- Spectral
- Linting
- API Governance
---
