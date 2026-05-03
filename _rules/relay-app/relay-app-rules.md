---
api_specs:
- filename: relay-app-openapi.yml
  format: yaml
  label: Relay App Automation API
  slug: relay-app-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/relay-app/refs/heads/main/openapi/relay-app-openapi.yml
categories:
- relay
description: Spectral linting rules defining API design standards and conventions for Relay App.
layout: rules
name: Relay App API Rules
provider_name: Relay App
provider_slug: relay-app
rule_count: 10
rules:
- description: All paths should be prefixed with /v1/ for API versioning.
  given: $.paths
  name: relay-app-versioned-paths
  severity: warn
- description: Webhook paths should include a webhookId path parameter.
  given: $.paths[?(@property =~ /webhook/)]
  name: relay-app-webhook-id-required
  severity: warn
- description: All operations must have unique operationIds in camelCase.
  given: $.paths[*][*]
  name: relay-app-operation-ids
  severity: error
- description: OperationIds should use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: relay-app-operation-id-camel-case
  severity: warn
- description: Operation summaries should use Title Case.
  given: $.paths[*][*].summary
  name: relay-app-title-case-summaries
  severity: warn
- description: All operations should have at least one tag for grouping.
  given: $.paths[*][*]
  name: relay-app-operation-tags
  severity: error
- description: All response objects should include a description.
  given: $.paths[*][*].responses[*]
  name: relay-app-response-descriptions
  severity: warn
- description: Status-related fields should use enum values for type safety.
  given: $.components.schemas[*].properties.status
  name: relay-app-status-enum
  severity: info
- description: Webhook trigger responses should include a runId field for tracking.
  given: $.components.schemas.WebhookTriggerResponse.properties
  name: relay-app-webhook-response-run-id
  severity: warn
- description: Path segments should use kebab-case.
  given: $.paths
  name: relay-app-kebab-case-paths
  severity: warn
rules_file: rules/relay-app-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/relay-app/refs/heads/main/rules/relay-app-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: relay-app-rules
source_filename: relay-app-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # Relay App uses /v1/ versioned paths\n  relay-app-versioned-paths:\n    description: All paths should be prefixed with /v1/ for API versioning.\n    message: \"Path '{{property}}' should start with /v1/.\"\n    given: \"$.paths\"\n    severity: warn\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/v1/.*\"\n\n  # Webhook paths should include a webhookId parameter\n  relay-app-webhook-id-required:\n    description: Webhook paths should include a webhookId path parameter.\n    message: \"Webhook path '{{property}}' should include {webhookId} path parameter.\"\n    given: \"$.paths[?(@property =~ /webhook/)]\"\n    severity: warn\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{webhookId\\\\}.*\"\n\n  # All operations must have operationIds\n  relay-app-operation-ids:\n    description: All operations must have unique operationIds\
  \ in camelCase.\n    message: \"Operation at '{{path}}' is missing an operationId.\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  # OperationIds should be camelCase\n  relay-app-operation-id-camel-case:\n    description: OperationIds should use camelCase naming convention.\n    message: \"OperationId '{{value}}' should use camelCase.\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries should use Title Case\n  relay-app-title-case-summaries:\n    description: Operation summaries should use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # All operations must have at least one tag\n  relay-app-operation-tags:\n\
  \    description: All operations should have at least one tag for grouping.\n    message: \"Operation '{{path}}' is missing tags.\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  # All responses should have descriptions\n  relay-app-response-descriptions:\n    description: All response objects should include a description.\n    message: \"Response '{{path}}' is missing a description.\"\n    given: \"$.paths[*][*].responses[*]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # Status fields should use enum values\n  relay-app-status-enum:\n    description: Status-related fields should use enum values for type safety.\n    message: \"Schema property '{{path}}' named 'status' should define enum values.\"\n    given: \"$.components.schemas[*].properties.status\"\n    severity: info\n    then:\n      field: enum\n      function: truthy\n\n  # Webhook trigger responses should include runId\n\
  \  relay-app-webhook-response-run-id:\n    description: Webhook trigger responses should include a runId field for tracking.\n    message: \"Webhook response schema should include a runId property.\"\n    given: \"$.components.schemas.WebhookTriggerResponse.properties\"\n    severity: warn\n    then:\n      field: runId\n      function: truthy\n\n  # Paths should use kebab-case\n  relay-app-kebab-case-paths:\n    description: Path segments should use kebab-case.\n    message: \"Path '{{property}}' should use kebab-case segments.\"\n    given: \"$.paths\"\n    severity: warn\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z_]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/relay-app/refs/heads/main/rules/relay-app-rules.yml
tags:
- Automation
- Workflow
- Integration
- No-Code
- AI
- Webhooks
- Spectral
- Linting
- API Governance
---
