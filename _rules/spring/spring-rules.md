---
api_specs:
- filename: spring-boot-actuator-openapi.yml
  format: yaml
  label: Spring Boot Actuator API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring/refs/heads/main/openapi/spring-boot-actuator-openapi.yml
- filename: spring-initializr-api-openapi.yml
  format: yaml
  label: Spring Initializr API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring/refs/heads/main/openapi/spring-initializr-api-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Framework.
layout: rules
name: Spring Framework API Rules
provider_name: Spring Framework
provider_slug: spring
rule_count: 11
rules:
- description: Spring Boot Actuator endpoints should support the vendor media type
  given: $.paths['/health'][get].responses['200'].content
  name: spring-actuator-content-type
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: spring-operation-id-required
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: spring-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: spring-operation-summary-required
  severity: warn
- description: Operation summaries should use Title Case
  given: $.paths[*][*].summary
  name: spring-operation-summary-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][*]
  name: spring-operation-description-required
  severity: warn
- description: All operations should have tags
  given: $.paths[*][*]
  name: spring-operation-tags-required
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spring-tags-title-case
  severity: warn
- description: Spring APIs should define security schemes when authentication is used
  given: $.components
  name: spring-security-scheme-defined
  severity: warn
- description: Operations must define at least one 2xx response
  given: $.paths[*][*].responses
  name: spring-success-response-required
  severity: error
- description: Path parameters should have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: spring-path-param-described
  severity: warn
rules_file: rules/spring-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring/refs/heads/main/rules/spring-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 8
slug: spring-rules
source_filename: spring-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Spring APIs use the actuator content type for HAL responses\n  spring-actuator-content-type:\n    description: Spring Boot Actuator endpoints should support the vendor media type\n    message: >-\n      Actuator endpoints should support application/vnd.spring-boot.actuator.v3+json\n    severity: info\n    given: $.paths['/health'][get].responses['200'].content\n    then:\n      field: 'application/vnd.spring-boot.actuator.v3+json'\n      function: defined\n\n  # All operations require operationId\n  spring-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: $.paths[*][*]\n    then:\n      field: operationId\n      function: defined\n\n  # Operation IDs should follow camelCase\n  spring-operation-id-camel-case:\n    description: Operation IDs should use camelCase\n    message: 'Operation ID \"{{value}}\" should use camelCase'\n    severity:\
  \ warn\n    given: $.paths[*][*].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  # All operations must have summaries\n  spring-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: summary\n      function: defined\n\n  # Summaries should use Title Case (Spring style)\n  spring-operation-summary-title-case:\n    description: Operation summaries should use Title Case\n    message: 'Summary \"{{value}}\" should use Title Case'\n    severity: warn\n    given: $.paths[*][*].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(\\s[A-Z][a-zA-Z0-9]*)*$'\n\n  # Operations should have descriptions\n  spring-operation-description-required:\n    description: All operations should have a description\n    message: Operation is missing description\n\
  \    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: description\n      function: defined\n\n  # All operations should have tags\n  spring-operation-tags-required:\n    description: All operations should have tags\n    message: Operation is missing tags\n    severity: warn\n    given: $.paths[*][*]\n    then:\n      field: tags\n      function: defined\n\n  # Tags must use Title Case\n  spring-tags-title-case:\n    description: All tags must use Title Case\n    message: 'Tag \"{{value}}\" should use Title Case'\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(\\s[A-Z][a-zA-Z0-9]*)*$'\n\n  # Spring APIs should define security schemes\n  spring-security-scheme-defined:\n    description: Spring APIs should define security schemes when authentication is used\n    message: No security schemes defined in components\n    severity: warn\n    given: $.components\n    then:\n      field:\
  \ securitySchemes\n      function: defined\n\n  # Responses must define at least one success response\n  spring-success-response-required:\n    description: Operations must define at least one 2xx response\n    message: Operation has no 2xx success response defined\n    severity: error\n    given: $.paths[*][*].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required:\n                - '200'\n            - required:\n                - '201'\n            - required:\n                - '204'\n\n  # Path parameters must be described\n  spring-path-param-described:\n    description: Path parameters should have descriptions\n    message: Path parameter \"{{value}}\" is missing a description\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.in == 'path')]\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring/refs/heads/main/rules/spring-rules.yml
tags:
- AI
- Cloud Native
- Enterprise
- Framework
- Java
- Microservices
- Open Source
- REST
- Spring Boot
- Spectral
- Linting
- API Governance
---
