---
api_specs:
- filename: sinch-sms-openapi.yml
  format: yaml
  label: Sinch SMS API
  slug: sms-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-sms-openapi.yml
- filename: sinch-conversation-openapi.yml
  format: yaml
  label: Sinch Conversation API
  slug: conversation-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-conversation-openapi.yml
- filename: sinch-voice-openapi.yml
  format: yaml
  label: Sinch Voice API
  slug: voice-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-voice-openapi.yml
- filename: sinch-verification-openapi.yml
  format: yaml
  label: Sinch Verification API
  slug: verification-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-verification-openapi.yml
- filename: sinch-numbers-openapi.yml
  format: yaml
  label: Sinch Numbers API
  slug: numbers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-numbers-openapi.yml
- filename: sinch-fax-openapi.yml
  format: yaml
  label: Sinch Fax API
  slug: fax-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-fax-openapi.yml
- filename: sinch-elastic-sip-trunking-openapi.yml
  format: yaml
  label: Sinch Elastic SIP Trunking API
  slug: elastic-sip-trunking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-elastic-sip-trunking-openapi.yml
- filename: sinch-brands-openapi.yml
  format: yaml
  label: Sinch Brands API
  slug: brands-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-brands-openapi.yml
- filename: sinch-provisioning-openapi.yml
  format: yaml
  label: Sinch Provisioning API
  slug: provisioning-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-provisioning-openapi.yml
- filename: sinch-registration-openapi.yml
  format: yaml
  label: Sinch Registration API
  slug: registration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/openapi/sinch-registration-openapi.yml
categories:
- sinch
description: Spectral linting rules defining API design standards and conventions for Sinch.
layout: rules
name: Sinch API Rules
provider_name: Sinch
provider_slug: sinch
rule_count: 10
rules:
- description: All Sinch API operations must use Bearer token authentication
  given: $.paths.*.*.security
  name: sinch-bearer-auth
  severity: error
- description: All Sinch API paths must include a version segment (v1, v2, etc.)
  given: $.paths[*]~
  name: sinch-versioned-paths
  severity: error
- description: Resource paths should include project_id as a path parameter
  given: $.paths[?(@property.match(/projects/))]
  name: sinch-project-id-in-path
  severity: warn
- description: All operationId values must use camelCase
  given: $.paths.*.*.operationId
  name: sinch-camel-case-operation-ids
  severity: error
- description: All operation summaries must use Title Case
  given: $.paths.*.*.summary
  name: sinch-title-case-summaries
  severity: warn
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: sinch-tags-required
  severity: warn
- description: API info must include contact information
  given: $.info
  name: sinch-contact-info
  severity: warn
- description: API should include external documentation link
  given: $
  name: sinch-external-docs
  severity: info
- description: API info must include terms of service URL
  given: $.info
  name: sinch-terms-of-service
  severity: warn
- description: API must define at least one server
  given: $
  name: sinch-servers-defined
  severity: error
rules_file: rules/sinch-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/rules/sinch-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: sinch-rules
source_filename: sinch-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sinch-bearer-auth:\n    description: All Sinch API operations must use Bearer token authentication\n    message: \"Operation is missing bearerAuth security requirement\"\n    severity: error\n    given: \"$.paths.*.*.security\"\n    then:\n      function: truthy\n\n  sinch-versioned-paths:\n    description: All Sinch API paths must include a version segment (v1, v2, etc.)\n    message: \"API path '{{value}}' must include a version segment like /v1/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+/\"\n\n  sinch-project-id-in-path:\n    description: Resource paths should include project_id as a path parameter\n    message: \"Consider using project_id scoping in path parameters\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/projects/))]\"\n    then:\n      function: truthy\n\n  sinch-camel-case-operation-ids:\n    description: All operationId values must use camelCase\n\
  \    message: \"operationId '{{value}}' should use camelCase\"\n    severity: error\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sinch-title-case-summaries:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sinch-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  sinch-contact-info:\n    description: API info must include contact information\n    message: \"API info is missing contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sinch-external-docs:\n\
  \    description: API should include external documentation link\n    message: \"API is missing externalDocs reference\"\n    severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n\n  sinch-terms-of-service:\n    description: API info must include terms of service URL\n    message: \"API info is missing termsOfService\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: termsOfService\n      function: truthy\n\n  sinch-servers-defined:\n    description: API must define at least one server\n    message: \"API is missing server definitions\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sinch/refs/heads/main/rules/sinch-rules.yml
tags:
- Communications
- Messaging
- SMS
- Voice
- Verification
- CPaaS
- Spectral
- Linting
- API Governance
---
