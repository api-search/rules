---
api_specs:
- filename: spring-boot-admin-console-openapi.yml
  format: yaml
  label: Spring Boot Admin Server API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-boot-admin-console/refs/heads/main/openapi/spring-boot-admin-console-openapi.yml
categories:
- sba
description: Spectral linting rules defining API design standards and conventions for Spring Boot Admin Console.
layout: rules
name: Spring Boot Admin Console API Rules
provider_name: Spring Boot Admin Console
provider_slug: spring-boot-admin-console
rule_count: 8
rules:
- description: All Spring Boot Admin API operations must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: sba-operationid-required
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: sba-operationid-camelcase
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: sba-tags-required
  severity: error
- description: All GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: sba-get-response-200
  severity: error
- description: DELETE operations should return 204 No Content on success.
  given: $.paths[*].delete.responses
  name: sba-delete-response-204
  severity: warn
- description: All named schemas should have a description.
  given: $.components.schemas[*]
  name: sba-schema-description
  severity: warn
- description: Instance ID path parameters should be named 'id'.
  given: $.paths['/instances/{id}'][*].parameters[*]
  name: sba-instance-id-path-param
  severity: info
- description: Status fields in response schemas should define an enum of valid values.
  given: $.components.schemas[*].properties.status
  name: sba-status-enum-defined
  severity: warn
rules_file: rules/spring-boot-admin-console-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-boot-admin-console/refs/heads/main/rules/spring-boot-admin-console-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: spring-boot-admin-console-rules
source_filename: spring-boot-admin-console-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sba-operationid-required:\n    description: All Spring Boot Admin API operations must have an operationId.\n    message: \"OperationId is required for every operation.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sba-operationid-camelcase:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sba-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  sba-get-response-200:\n    description: All\
  \ GET operations must define a 200 response.\n    message: \"GET operation must define a 200 OK response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  sba-delete-response-204:\n    description: DELETE operations should return 204 No Content on success.\n    message: \"DELETE operation should define a 204 No Content response.\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  sba-schema-description:\n    description: All named schemas should have a description.\n    message: \"Schema '{{property}}' is missing a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  sba-instance-id-path-param:\n    description: Instance ID path parameters should be named 'id'.\n    message: \"Instance path parameter should be named 'id'.\"\n    severity: info\n   \
  \ given: \"$.paths['/instances/{id}'][*].parameters[*]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^id$\"\n\n  sba-status-enum-defined:\n    description: Status fields in response schemas should define an enum of valid values.\n    message: \"Status field should define valid Spring Boot Admin status enum values.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-boot-admin-console/refs/heads/main/rules/spring-boot-admin-console-rules.yml
tags:
- Actuator
- Administration
- Java
- Microservices
- Monitoring
- Spring Boot
- Spectral
- Linting
- API Governance
---
