---
api_specs:
- filename: strimzi-kafka-bridge-openapi.yml
  format: yaml
  label: Strimzi Kafka Bridge REST API
  slug: strimzi-kafka-bridge-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strimzi/refs/heads/main/openapi/strimzi-kafka-bridge-openapi.yml
categories:
- strimzi
description: Spectral linting rules defining API design standards and conventions for Strimzi.
layout: rules
name: Strimzi API Rules
provider_name: Strimzi
provider_slug: strimzi
rule_count: 8
rules:
- description: Strimzi Kafka Bridge operationIds use camelCase (e.g., send, createConsumer, poll, commit).
  given: $.paths[*][*].operationId
  name: strimzi-operation-ids-camel-case
  severity: warn
- description: All OpenAPI tags must use Title Case (e.g., 'Producer', 'Consumer', 'Topics', 'Seek').
  given: $.tags[*].name
  name: strimzi-tags-title-case
  severity: warn
- description: 'Strimzi Kafka Bridge uses Kafka-specific content types for producer and consumer endpoints. The content type format is: application/vnd.kafka.{format}.v2+json or application/vnd.kafka.v2+json.'
  given: $.paths['/topics/{topicname}'][post].requestBody.content
  name: strimzi-kafka-content-type
  severity: info
- description: Consumer group endpoints must use 'groupid' as the path parameter for the consumer group identifier.
  given: $.paths['/consumers/{groupid}'][*].parameters[*].name
  name: strimzi-consumer-group-path-param
  severity: warn
- description: DELETE operations return 204 No Content on success in the Kafka Bridge.
  given: $.paths[*][delete].responses
  name: strimzi-delete-returns-204
  severity: info
- description: The Kafka Bridge must document /healthy and /ready endpoints for Kubernetes liveness and readiness probes.
  given: $.paths
  name: strimzi-health-endpoints-documented
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: strimzi-operation-summaries-present
  severity: error
- description: Topic endpoints use 'topicname' as the path parameter name for consistency across Kafka Bridge endpoints.
  given: $.paths['/topics/{topicname}'][*].parameters[*].name
  name: strimzi-topic-name-path-param
  severity: info
rules_file: rules/strimzi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/strimzi/refs/heads/main/rules/strimzi-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 4
slug: strimzi-rules
source_filename: strimzi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  strimzi-operation-ids-camel-case:\n    description: >-\n      Strimzi Kafka Bridge operationIds use camelCase (e.g., send,\n      createConsumer, poll, commit).\n    message: \"OperationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  strimzi-tags-title-case:\n    description: >-\n      All OpenAPI tags must use Title Case (e.g., 'Producer', 'Consumer',\n      'Topics', 'Seek').\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  strimzi-kafka-content-type:\n    description: >-\n      Strimzi Kafka Bridge uses Kafka-specific content types for producer\n      and consumer endpoints. The content type format\
  \ is:\n      application/vnd.kafka.{format}.v2+json or application/vnd.kafka.v2+json.\n    message: \"Kafka Bridge endpoints should use Kafka content types\"\n    severity: info\n    given: \"$.paths['/topics/{topicname}'][post].requestBody.content\"\n    then:\n      function: truthy\n      field: \"application/vnd.kafka.json.v2+json\"\n\n  strimzi-consumer-group-path-param:\n    description: >-\n      Consumer group endpoints must use 'groupid' as the path parameter\n      for the consumer group identifier.\n    message: \"Consumer group path parameter must be named 'groupid'\"\n    severity: warn\n    given: \"$.paths['/consumers/{groupid}'][*].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^groupid$\"\n\n  strimzi-delete-returns-204:\n    description: >-\n      DELETE operations return 204 No Content on success in the Kafka Bridge.\n    message: \"DELETE operation should return 204 on success\"\n    severity: info\n    given: \"$.paths[*][delete].responses\"\
  \n    then:\n      function: truthy\n      field: \"204\"\n\n  strimzi-health-endpoints-documented:\n    description: >-\n      The Kafka Bridge must document /healthy and /ready endpoints for\n      Kubernetes liveness and readiness probes.\n    message: \"Health check endpoints /healthy and /ready must be documented\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: truthy\n      field: \"/healthy\"\n\n  strimzi-operation-summaries-present:\n    description: >-\n      All operations must have a summary.\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: truthy\n      field: \"summary\"\n\n  strimzi-topic-name-path-param:\n    description: >-\n      Topic endpoints use 'topicname' as the path parameter name\n      for consistency across Kafka Bridge endpoints.\n    message: \"Topic path parameter should be named 'topicname'\"\n    severity: info\n    given: \"$.paths['/topics/{topicname}'][*].parameters[*].name\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^topicname$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/strimzi/refs/heads/main/rules/strimzi-rules.yml
tags:
- Kafka
- Kubernetes
- Messaging
- Operator
- Streaming
- Spectral
- Linting
- API Governance
---
