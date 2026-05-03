---
api_specs:
- filename: spring-boot-3-actuator-openapi.yml
  format: yaml
  label: Spring Boot Actuator API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-boot-3/refs/heads/main/openapi/spring-boot-3-actuator-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Boot 3.
layout: rules
name: Spring Boot 3 API Rules
provider_name: Spring Boot 3
provider_slug: spring-boot-3
rule_count: 8
rules:
- description: All Spring Boot Actuator operations must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-boot-actuator-operationid-required
  severity: error
- description: OperationIds must use camelCase to match Spring Boot conventions.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-boot-actuator-operationid-camelcase
  severity: warn
- description: All operations must have at least one tag for API grouping.
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-boot-actuator-tags-required
  severity: error
- description: All GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: spring-boot-actuator-response-200-on-get
  severity: error
- description: All named schemas should have a description.
  given: $.components.schemas[*]
  name: spring-boot-actuator-schema-description
  severity: warn
- description: Health status fields should use Spring Boot's standard status values.
  given: $.components.schemas[*].properties.status
  name: spring-boot-actuator-health-status-enum
  severity: info
- description: POST operations that mutate state should define a request body.
  given: $.paths[*].post
  name: spring-boot-actuator-post-request-body
  severity: warn
- description: All path and query parameters must have descriptions.
  given: $.paths[*][*].parameters[*]
  name: spring-boot-actuator-parameter-description
  severity: warn
rules_file: rules/spring-boot-3-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-boot-3/refs/heads/main/rules/spring-boot-3-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: spring-boot-3-rules
source_filename: spring-boot-3-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-boot-actuator-operationid-required:\n    description: All Spring Boot Actuator operations must have an operationId.\n    message: \"OperationId is required for every actuator endpoint operation.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spring-boot-actuator-operationid-camelcase:\n    description: OperationIds must use camelCase to match Spring Boot conventions.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spring-boot-actuator-tags-required:\n    description: All operations must have at least one tag for API grouping.\n    message: \"Operation must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  spring-boot-actuator-response-200-on-get:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation must define a 200 OK response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  spring-boot-actuator-schema-description:\n    description: All named schemas should have a description.\n    message: \"Schema '{{property}}' is missing a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spring-boot-actuator-health-status-enum:\n    description: Health status fields should use Spring Boot's standard status values.\n    message: \"Health status should be UP, DOWN, OUT_OF_SERVICE, or UNKNOWN.\"\n    severity: info\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  spring-boot-actuator-post-request-body:\n\
  \    description: POST operations that mutate state should define a request body.\n    message: \"POST operation should define a requestBody for mutation operations.\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  spring-boot-actuator-parameter-description:\n    description: All path and query parameters must have descriptions.\n    message: \"Parameter '{{value}}' is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-boot-3/refs/heads/main/rules/spring-boot-3-rules.yml
tags:
- Enterprise
- Framework
- Java
- Microservices
- REST API
- Spring Boot
- Spectral
- Linting
- API Governance
---
