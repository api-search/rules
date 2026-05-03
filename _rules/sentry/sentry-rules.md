---
api_specs:
- filename: sentry-api-openapi.yml
  format: yaml
  label: Sentry Error Monitoring API
  slug: sentry-error-monitoring-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/openapi/sentry-api-openapi.yml
- filename: sentry-webhooks-asyncapi.yml
  format: yaml
  label: Sentry Integration Platform API
  slug: sentry-integration-platform-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/asyncapi/sentry-webhooks-asyncapi.yml
categories:
- sentry
description: Spectral linting rules defining API design standards and conventions for Sentry.
layout: rules
name: Sentry API Rules
provider_name: Sentry
provider_slug: sentry
rule_count: 13
rules:
- description: Sentry API paths must end with a trailing slash
  given: $.paths[*]~
  name: sentry-paths-trailing-slash
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sentry-operation-id-required
  severity: error
- description: Sentry operationIds use camelCase (listIssues, createRelease, etc.)
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sentry-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sentry-operation-summary-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: sentry-operation-description-required
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: sentry-operation-tags-required
  severity: error
- description: Operations must use tags from the defined tag list
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: sentry-valid-tags
  severity: warn
- description: organization_slug path parameter should use $ref to the shared parameter definition
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name=='organization_slug')]
  name: sentry-org-slug-ref
  severity: warn
- description: GET operations returning arrays should include cursor and limit pagination parameters
  given: $.paths[*].get
  name: sentry-list-operations-pagination
  severity: info
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: sentry-parameter-description
  severity: warn
- description: Operations must define at least one success response (200 or 201)
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sentry-response-success-required
  severity: error
- description: Sentry API requires authentication on all endpoints
  given: $
  name: sentry-security-defined
  severity: error
- description: API must define reusable schemas in components
  given: $.components
  name: sentry-components-schemas-defined
  severity: warn
rules_file: rules/sentry-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/rules/sentry-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 7
slug: sentry-rules
source_filename: sentry-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Sentry API uses trailing slashes on all paths\n  sentry-paths-trailing-slash:\n    description: Sentry API paths must end with a trailing slash\n    message: \"Path '{{value}}' must end with a trailing slash (/)\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/$\"\n\n  # All operations must have an operationId\n  sentry-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # operationId must use camelCase\n  sentry-operation-id-camel-case:\n    description: Sentry operationIds use camelCase (listIssues, createRelease, etc.)\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have a summary\n  sentry-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # All operations must have a description\n  sentry-operation-description-required:\n    description: All operations must have a description\n    message: \"Operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: defined\n\n  # All operations must have at least one tag\n  sentry-operation-tags-required:\n    description: All operations must be tagged\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  # Tags must match defined tags in the root tags object\n  sentry-valid-tags:\n    description: Operations must use tags from the defined tag list\n    message: \"Tag '{{value}}' is not in the global tags list\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Alerts\n          - Events\n          - Issues\n          - Organizations\n          - Projects\n          - Releases\n\n  # organization_slug path parameter must use $ref\n  sentry-org-slug-ref:\n    description: organization_slug path parameter should use $ref to the shared parameter definition\n    message: \"organization_slug parameter should use $ref: '#/components/parameters/OrganizationSlug'\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name=='organization_slug')]\"\
  \n    then:\n      field: \"$ref\"\n      function: defined\n\n  # GET list operations should support pagination\n  sentry-list-operations-pagination:\n    description: GET operations returning arrays should include cursor and limit pagination parameters\n    message: \"List operation should support limit and cursor pagination\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n          required:\n            - parameters\n\n  # All parameters must have descriptions\n  sentry-parameter-description:\n    description: All parameters must have descriptions\n    message: \"Parameter '{{value}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: defined\n\n  # Responses must define at least 200/201 and 4xx\n  sentry-response-success-required:\n\
  \    description: Operations must define at least one success response (200 or 201)\n    message: \"Operation must have a 200 or 201 response defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n\n  # Security must be defined at operation or global level\n  sentry-security-defined:\n    description: Sentry API requires authentication on all endpoints\n    message: \"Global security scheme must be defined\"\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: defined\n\n  # Schema components must be defined for reusable objects\n  sentry-components-schemas-defined:\n    description: API must define reusable schemas in components\n    message: \"components.schemas must be defined\"\n    severity: warn\n    given:\
  \ \"$.components\"\n    then:\n      field: schemas\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sentry/refs/heads/main/rules/sentry-rules.yml
tags:
- Error Monitoring
- Debugging
- Observability
- Application Performance Management
- Developer Tools
- Spectral
- Linting
- API Governance
---
