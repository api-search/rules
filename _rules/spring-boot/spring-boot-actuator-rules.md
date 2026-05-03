---
api_specs:
- filename: spring-boot-actuator-openapi.yml
  format: yaml
  label: Spring Boot Actuator API
  slug: spring-boot-actuator
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-boot/refs/heads/main/openapi/spring-boot-actuator-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Boot.
layout: rules
name: Spring Boot API Rules
provider_name: Spring Boot
provider_slug: spring-boot
rule_count: 9
rules:
- description: Actuator operation IDs should be descriptive and use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-boot-actuator-operation-id-prefix
  severity: warn
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: spring-boot-actuator-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-boot-actuator-tags-defined
  severity: error
- description: All tags must use Title Case
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: spring-boot-actuator-tags-title-case
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: spring-boot-actuator-response-200-defined
  severity: error
- description: Actuator endpoint paths should use lowercase with hyphens
  given: $.paths
  name: spring-boot-actuator-path-lowercase-kebab
  severity: warn
- description: Paths must not end with a trailing slash
  given: $.paths
  name: spring-boot-actuator-no-trailing-slash
  severity: error
- description: API info must include contact information
  given: $.info
  name: spring-boot-actuator-info-contact-defined
  severity: warn
- description: At least one server must be defined
  given: $
  name: spring-boot-actuator-servers-defined
  severity: error
rules_file: rules/spring-boot-actuator-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-boot/refs/heads/main/rules/spring-boot-actuator-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: spring-boot-actuator-rules
source_filename: spring-boot-actuator-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  spring-boot-actuator-operation-id-prefix:\n    description: Actuator operation IDs should be descriptive and use camelCase\n    message: \"Operation ID '{{value}}' should be camelCase and descriptive (e.g., getHealth, listMetrics)\"\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  spring-boot-actuator-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][^a-z]*([A-Z][^a-z]*)*\"\n\n  spring-boot-actuator-tags-defined:\n    description: All operations must have at least one tag\n    message: \"Operation '{{path}}' is missing tags\"\n    given: \"\
  $.paths[*][get,post,put,delete,patch]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  spring-boot-actuator-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' should be in Title Case (e.g., 'Health', 'Metrics', 'Environment')\"\n    given: \"$.paths[*][get,post,put,delete,patch].tags[*]\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  spring-boot-actuator-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: \"GET operation at '{{path}}' must define a 200 response\"\n    given: \"$.paths[*].get\"\n    severity: error\n    then:\n      field: responses.200\n      function: truthy\n\n  spring-boot-actuator-path-lowercase-kebab:\n    description: Actuator endpoint paths should use lowercase with hyphens\n    message: \"Path '{{path}}' should use lowercase kebab-case\"\n    given: \"$.paths\"\n\
  \    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/[a-z0-9\\\\-\\\\/\\\\{\\\\}]*$\"\n\n  spring-boot-actuator-no-trailing-slash:\n    description: Paths must not end with a trailing slash\n    message: \"Path '{{path}}' must not end with a trailing slash\"\n    given: \"$.paths\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*\\\\/$\"\n\n  spring-boot-actuator-info-contact-defined:\n    description: API info must include contact information\n    message: \"API info must include a contact block with name and url\"\n    given: \"$.info\"\n    severity: warn\n    then:\n      field: contact\n      function: truthy\n\n  spring-boot-actuator-servers-defined:\n    description: At least one server must be defined\n    message: \"OpenAPI spec must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-boot/refs/heads/main/rules/spring-boot-actuator-rules.yml
tags:
- Auto Configuration
- Embedded Server
- Framework
- Java
- Microservices
- REST API
- Spring
- Web Development
- Spectral
- Linting
- API Governance
---
