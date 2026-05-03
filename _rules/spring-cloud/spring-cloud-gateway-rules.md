---
api_specs:
- filename: spring-cloud-gateway-actuator-openapi.yml
  format: yaml
  label: Spring Cloud Gateway
  slug: spring-cloud-gateway
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-cloud/refs/heads/main/openapi/spring-cloud-gateway-actuator-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Cloud.
layout: rules
name: Spring Cloud API Rules
provider_name: Spring Cloud
provider_slug: spring-cloud
rule_count: 7
rules:
- description: Operation IDs must be camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-cloud-operation-id-camel-case
  severity: warn
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: spring-cloud-summary-title-case
  severity: warn
- description: All operations must declare at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-cloud-tags-required
  severity: error
- description: Tags must be Title Case
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: spring-cloud-tags-title-case
  severity: warn
- description: API should define schemas for core resources
  given: $.components
  name: spring-cloud-components-schemas-defined
  severity: warn
- description: At least one server must be defined
  given: $
  name: spring-cloud-servers-defined
  severity: error
- description: API info must include a version
  given: $.info
  name: spring-cloud-info-version-defined
  severity: error
rules_file: rules/spring-cloud-gateway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud/refs/heads/main/rules/spring-cloud-gateway-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: spring-cloud-gateway-rules
source_filename: spring-cloud-gateway-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  spring-cloud-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  spring-cloud-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-cloud-tags-required:\n    description: All operations must declare at least one tag\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  spring-cloud-tags-title-case:\n\
  \    description: Tags must be Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].tags[*]\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  spring-cloud-components-schemas-defined:\n    description: API should define schemas for core resources\n    message: \"API should define reusable schemas in components.schemas\"\n    given: \"$.components\"\n    severity: warn\n    then:\n      field: schemas\n      function: truthy\n\n  spring-cloud-servers-defined:\n    description: At least one server must be defined\n    message: \"OpenAPI spec must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n\n  spring-cloud-info-version-defined:\n    description: API info must include a version\n    message: \"API must specify a version in info.version\"\n    given: \"$.info\"\n    severity:\
  \ error\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud/refs/heads/main/rules/spring-cloud-gateway-rules.yml
tags:
- Circuit Breaker
- Cloud Native
- Distributed Systems
- Java
- Microservices
- Service Discovery
- Spring Framework
- Spectral
- Linting
- API Governance
---
