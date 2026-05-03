---
api_specs:
- filename: spring-integration-http-openapi.yml
  format: yaml
  label: Spring Integration HTTP Adapter API
  slug: spring-integration-http
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-integration/refs/heads/main/openapi/spring-integration-http-openapi.yml
- filename: spring-integration-management-openapi.yml
  format: yaml
  label: Spring Integration Management API
  slug: spring-integration-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-integration/refs/heads/main/openapi/spring-integration-management-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Integration.
layout: rules
name: Spring Integration API Rules
provider_name: Spring Integration
provider_slug: spring-integration
rule_count: 5
rules:
- description: All operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-integration-operation-id
  severity: error
- description: Operations must include at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-integration-tags-required
  severity: warn
- description: Summaries must use Title Case
  given: $.paths[*][*].summary
  name: spring-integration-summary-title-case
  severity: warn
- description: Management API paths should be descriptive and use kebab-case
  given: $.paths
  name: spring-integration-management-paths
  severity: info
- description: All responses should have descriptions
  given: $.paths[*][*].responses[*]
  name: spring-integration-response-descriptions
  severity: warn
rules_file: rules/spring-integration-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-integration/refs/heads/main/rules/spring-integration-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 3
slug: spring-integration-rules
source_filename: spring-integration-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-integration-operation-id:\n    description: All operations must have operationId\n    message: \"Missing operationId at {{path}}\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spring-integration-tags-required:\n    description: Operations must include at least one tag\n    message: \"Operation at {{path}} must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spring-integration-summary-title-case:\n    description: Summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-integration-management-paths:\n    description: Management API paths should be descriptive\
  \ and use kebab-case\n    message: \"Path should use kebab-case segments\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-zA-Z0-9]*({[^}]+})?)*$\"\n\n  spring-integration-response-descriptions:\n    description: All responses should have descriptions\n    message: \"Response at {{path}} is missing description\"\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-integration/refs/heads/main/rules/spring-integration-rules.yml
tags:
- AMQP
- Enterprise Integration
- Event-Driven
- Integration Patterns
- Java
- Messaging
- Spring
- Spectral
- Linting
- API Governance
---
