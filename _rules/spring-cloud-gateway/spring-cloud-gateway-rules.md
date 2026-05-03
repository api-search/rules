---
api_specs:
- filename: spring-cloud-gateway-actuator-openapi.yml
  format: yaml
  label: Spring Cloud Gateway Actuator API
  slug: spring-cloud-gateway-actuator
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-gateway/refs/heads/main/openapi/spring-cloud-gateway-actuator-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Cloud Gateway.
layout: rules
name: Spring Cloud Gateway API Rules
provider_name: Spring Cloud Gateway
provider_slug: spring-cloud-gateway
rule_count: 9
rules:
- description: Operation IDs must be camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-cloud-gateway-operation-id-camel-case
  severity: warn
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: spring-cloud-gateway-summary-title-case
  severity: warn
- description: All operations must declare at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-cloud-gateway-tags-required
  severity: error
- description: Tags must be Title Case
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: spring-cloud-gateway-tags-title-case
  severity: warn
- description: Route definitions must include an id field
  given: $.components.schemas.RouteDefinition
  name: spring-cloud-gateway-route-id-required
  severity: error
- description: Route definitions must include a uri field
  given: $.components.schemas.RouteDefinition
  name: spring-cloud-gateway-route-uri-required
  severity: error
- description: At least one server must be defined
  given: $
  name: spring-cloud-gateway-servers-defined
  severity: error
- description: All path parameters must have a description
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in == 'path')]
  name: spring-cloud-gateway-path-parameters-described
  severity: warn
- description: DELETE operations must define response codes
  given: $.paths[*].delete
  name: spring-cloud-gateway-delete-responses-defined
  severity: warn
rules_file: rules/spring-cloud-gateway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-gateway/refs/heads/main/rules/spring-cloud-gateway-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: spring-cloud-gateway-rules
source_filename: spring-cloud-gateway-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  spring-cloud-gateway-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  spring-cloud-gateway-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-cloud-gateway-tags-required:\n    description: All operations must declare at least one tag\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    severity: error\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  spring-cloud-gateway-tags-title-case:\n    description: Tags must be Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    given: \"$.paths[*][get,post,put,delete,patch].tags[*]\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  spring-cloud-gateway-route-id-required:\n    description: Route definitions must include an id field\n    message: \"Route definition schema must require an 'id' field\"\n    given: \"$.components.schemas.RouteDefinition\"\n    severity: error\n    then:\n      field: required\n      function: truthy\n\n  spring-cloud-gateway-route-uri-required:\n    description: Route definitions must include a uri field\n    message: \"Route definition schema must require a 'uri' field\"\n    given: \"$.components.schemas.RouteDefinition\"\n    severity: error\n    then:\n      field: required\n      function: truthy\n\n  spring-cloud-gateway-servers-defined:\n    description:\
  \ At least one server must be defined\n    message: \"OpenAPI spec must define at least one server\"\n    given: \"$\"\n    severity: error\n    then:\n      field: servers\n      function: truthy\n\n  spring-cloud-gateway-path-parameters-described:\n    description: All path parameters must have a description\n    message: \"Path parameter '{{value}}' is missing a description\"\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[?(@.in == 'path')]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  spring-cloud-gateway-delete-responses-defined:\n    description: DELETE operations must define response codes\n    message: \"DELETE operation should define both 200 (success) and 404 (not found) responses\"\n    given: \"$.paths[*].delete\"\n    severity: warn\n    then:\n      field: responses\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-cloud-gateway/refs/heads/main/rules/spring-cloud-gateway-rules.yml
tags:
- API Gateway
- Circuit Breaker
- Load Balancing
- Microservices
- Rate Limiting
- Routing
- Spring
- Spring WebFlux
- Spectral
- Linting
- API Governance
---
