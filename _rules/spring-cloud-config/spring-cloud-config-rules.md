---
api_specs:
- filename: spring-cloud-config-server-api.yml
  format: yaml
  label: Spring Cloud Config Server API
  slug: spring-cloud-config-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-config/refs/heads/main/openapi/spring-cloud-config-server-api.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Cloud Config.
layout: rules
name: Spring Cloud Config API Rules
provider_name: Spring Cloud Config
provider_slug: spring-cloud-config
rule_count: 8
rules:
- description: Operation IDs must be camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-cloud-config-operation-id-camel-case
  severity: warn
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: spring-cloud-config-summary-title-case
  severity: warn
- description: All operations must declare at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-cloud-config-tags-required
  severity: error
- description: Tags must be Title Case
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: spring-cloud-config-tags-title-case
  severity: warn
- description: All path parameters must have a description
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in == 'path')]
  name: spring-cloud-config-path-parameters-described
  severity: warn
- description: GET operations returning JSON must specify content type
  given: $.paths[*].get.responses.200
  name: spring-cloud-config-response-content-type
  severity: warn
- description: API must define security schemes
  given: $.components.securitySchemes
  name: spring-cloud-config-security-defined
  severity: warn
- description: At least one server must be defined
  given: $
  name: spring-cloud-config-servers-defined
  severity: error
rules_file: rules/spring-cloud-config-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-config/refs/heads/main/rules/spring-cloud-config-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: spring-cloud-config-rules
source_filename: spring-cloud-config-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  spring-cloud-config-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  spring-cloud-config-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-cloud-config-tags-required:\n    description: All operations must declare at least one tag\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    severity: error\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  spring-cloud-config-tags-title-case:\n    description: Tags must be Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].tags[*]\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  spring-cloud-config-path-parameters-described:\n    description: All path parameters must have a description\n    message: \"Path parameter '{{value}}' is missing a description\"\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[?(@.in == 'path')]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  spring-cloud-config-response-content-type:\n    description: GET operations returning JSON must specify content type\n    message: \"GET operation should specify application/json or application/x-yaml response content type\"\n    given: \"$.paths[*].get.responses.200\"\n    severity: warn\n    then:\n      field: content\n\
  \      function: truthy\n\n  spring-cloud-config-security-defined:\n    description: API must define security schemes\n    message: \"API must define at least one security scheme for Config Server authentication\"\n    given: \"$.components.securitySchemes\"\n    severity: warn\n    then:\n      function: truthy\n\n  spring-cloud-config-servers-defined:\n    description: At least one server must be defined\n    message: \"OpenAPI spec must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-config/refs/heads/main/rules/spring-cloud-config-rules.yml
tags:
- Configuration Management
- Distributed Systems
- Externalized Configuration
- Git
- Java
- Microservices
- Spring
- Spring Cloud
- Spectral
- Linting
- API Governance
---
