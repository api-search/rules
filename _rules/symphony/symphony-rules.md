---
api_specs:
- filename: symphony-pod-api-openapi.yml
  format: yaml
  label: Symphony Pod API
  slug: symphony-pod-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/symphony-pod-api-openapi.yml
- filename: agent-openapi-original.yml
  format: yaml
  label: Symphony Agent API
  slug: symphony-agent-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/agent-openapi-original.yml
- filename: authenticator-openapi-original.yml
  format: yaml
  label: Symphony Authenticator API
  slug: symphony-authenticator-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/authenticator-openapi-original.yml
- filename: login-openapi-original.yml
  format: yaml
  label: Symphony Login API
  slug: symphony-login-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/login-openapi-original.yml
- filename: profile-manager-openapi-original.yml
  format: yaml
  label: Symphony Profile Manager API
  slug: symphony-profile-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/profile-manager-openapi-original.yml
- filename: community-connect-openapi-original.yml
  format: yaml
  label: Symphony Community Connect API
  slug: symphony-community-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/openapi/community-connect-openapi-original.yml
categories:
- symphony
description: Spectral linting rules defining API design standards and conventions for Symphony.
layout: rules
name: Symphony API Rules
provider_name: Symphony
provider_slug: symphony
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: symphony-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: symphony-operation-has-operation-id
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: symphony-operation-has-tags
  severity: warn
- description: Symphony APIs require sessionToken header on authenticated endpoints
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name == 'sessionToken')]
  name: symphony-session-token-header
  severity: hint
- description: Operations should define error responses (4xx/5xx)
  given: $.paths[*][get,post,put,delete,patch].responses
  name: symphony-error-response-defined
  severity: warn
- description: Symphony API paths should be versioned with /v{n}/ prefix
  given: $.paths
  name: symphony-v-prefixed-paths
  severity: warn
- description: API paths must not have trailing slashes
  given: $.paths
  name: symphony-no-trailing-slash
  severity: warn
- description: All operations must define a 200 or 2xx success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: symphony-response-200-defined
  severity: error
- description: API info should include contact information
  given: $.info
  name: symphony-info-contact
  severity: warn
- description: API must define at least one server
  given: $
  name: symphony-server-defined
  severity: warn
rules_file: rules/symphony-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/rules/symphony-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 7
slug: symphony-rules
source_filename: symphony-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  symphony-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  symphony-operation-has-operation-id:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  symphony-operation-has-tags:\n    description: All operations must have at least one tag\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  symphony-session-token-header:\n    description: Symphony APIs require sessionToken header\
  \ on authenticated endpoints\n    message: Authenticated operations should reference sessionToken parameter\n    severity: hint\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[?(@.name == 'sessionToken')]\"\n    then:\n      field: in\n      function: enumeration\n      functionOptions:\n        values:\n          - header\n\n  symphony-error-response-defined:\n    description: Operations should define error responses (4xx/5xx)\n    message: Operation is missing error response definitions\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"500\"]\n\n  symphony-v-prefixed-paths:\n    description: Symphony API paths should be versioned with /v{n}/ prefix\n    message: \"Path '{{property}}' should start with a version prefix\
  \ (e.g. /v1/)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v[0-9]\"\n\n  symphony-no-trailing-slash:\n    description: API paths must not have trailing slashes\n    message: \"Path '{{property}}' must not have a trailing slash\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  symphony-response-200-defined:\n    description: All operations must define a 200 or 2xx success response\n    message: Operation is missing a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  symphony-info-contact:\n    description: API info should include contact information\n    message:\
  \ API info is missing contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  symphony-server-defined:\n    description: API must define at least one server\n    message: API is missing server definitions\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/symphony/refs/heads/main/rules/symphony-rules.yml
tags:
- Collaboration
- Communication
- Financial Services
- Messaging
- Secure Communication
- Spectral
- Linting
- API Governance
---
