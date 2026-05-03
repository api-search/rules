---
api_specs:
- filename: telegram-bot-openapi.yml
  format: yaml
  label: Telegram Bot API
  slug: telegram-bot-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/telegram/refs/heads/main/openapi/telegram-bot-openapi.yml
categories:
- telegram
description: Spectral linting rules defining API design standards and conventions for Telegram.
layout: rules
name: Telegram API Rules
provider_name: Telegram
provider_slug: telegram
rule_count: 13
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: telegram-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: telegram-operation-must-have-tag
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: telegram-operation-must-have-description
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: telegram-operation-must-have-operationid
  severity: error
- description: Operation IDs must use camelCase (Telegram method naming convention)
  given: $.paths[*][*].operationId
  name: telegram-operationid-camelcase
  severity: warn
- description: All operations must define a 200 response
  given: $.paths[*][*].responses
  name: telegram-response-200-required
  severity: error
- description: All 200 responses must have a content schema
  given: $.paths[*][*].responses.200
  name: telegram-response-must-have-schema
  severity: warn
- description: All schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: telegram-schema-must-have-description
  severity: info
- description: All request bodies must have a schema
  given: $.paths[*][*].requestBody.content[*]
  name: telegram-request-body-must-have-schema
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: telegram-no-empty-descriptions
  severity: warn
- description: API info must have a title
  given: $.info
  name: telegram-info-title-required
  severity: error
- description: API info must have a version
  given: $.info
  name: telegram-info-version-required
  severity: error
- description: API must define at least one server
  given: $
  name: telegram-servers-required
  severity: warn
rules_file: rules/telegram-bot-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/telegram/refs/heads/main/rules/telegram-bot-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 6
slug: telegram-bot-rules
source_filename: telegram-bot-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  telegram-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  telegram-operation-must-have-tag:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  telegram-operation-must-have-description:\n    description: All operations should have a description\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  telegram-operation-must-have-operationid:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n\
  \      function: truthy\n\n  telegram-operationid-camelcase:\n    description: Operation IDs must use camelCase (Telegram method naming convention)\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  telegram-response-200-required:\n    description: All operations must define a 200 response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  telegram-response-must-have-schema:\n    description: All 200 responses must have a content schema\n    severity: warn\n    given: \"$.paths[*][*].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  telegram-schema-must-have-description:\n    description: All schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n\
  \      field: description\n      function: truthy\n\n  telegram-request-body-must-have-schema:\n    description: All request bodies must have a schema\n    severity: error\n    given: \"$.paths[*][*].requestBody.content[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  telegram-no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    message: \"Description cannot be empty\"\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  telegram-info-title-required:\n    description: API info must have a title\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  telegram-info-version-required:\n    description: API info must have a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  telegram-servers-required:\n    description: API must define at least one server\n\
  \    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/telegram/refs/heads/main/rules/telegram-bot-rules.yml
tags:
- Bots
- Chat
- Messaging
- Notifications
- Payments
- Telegram
- Spectral
- Linting
- API Governance
---
