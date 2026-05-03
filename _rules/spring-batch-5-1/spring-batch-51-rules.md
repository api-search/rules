---
api_specs:
- filename: spring-batch-51-openapi.yml
  format: yaml
  label: Spring Batch 5.1 Core API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-batch-5-1/refs/heads/main/openapi/spring-batch-51-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Batch 5.1.
layout: rules
name: Spring Batch 5.1 API Rules
provider_name: Spring Batch 5.1
provider_slug: spring-batch-5-1
rule_count: 8
rules:
- description: All Spring Batch Actuator paths must be prefixed with /actuator or reflect the configured management base path.
  given: $.paths[*]~
  name: spring-batch-actuator-path-prefix
  severity: warn
- description: All operations must have at least one tag for grouping in the Batch Actuator API.
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-batch-operation-tags-required
  severity: error
- description: All operations in the Spring Batch Actuator API must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: spring-batch-operationid-required
  severity: error
- description: OperationIds must use camelCase to match Spring Batch conventions.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: spring-batch-operationid-camelcase
  severity: warn
- description: All GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: spring-batch-response-200-required
  severity: error
- description: All named schemas should have a description to support batch domain documentation.
  given: $.components.schemas[*]
  name: spring-batch-schema-description
  severity: warn
- description: Batch status fields should use the standard Spring Batch status enum values.
  given: $.components.schemas[*].properties.status
  name: spring-batch-status-enum
  severity: info
- description: Paginated responses should include page, size, totalElements, and totalPages.
  given: $.components.schemas[?(@.description =~ /[Pp]aginated/)]
  name: spring-batch-pagination-consistency
  severity: warn
rules_file: rules/spring-batch-51-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-batch-5-1/refs/heads/main/rules/spring-batch-51-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: spring-batch-51-rules
source_filename: spring-batch-51-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-batch-actuator-path-prefix:\n    description: All Spring Batch Actuator paths must be prefixed with /actuator or reflect the configured management base path.\n    message: \"{{description}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/\"\n\n  spring-batch-operation-tags-required:\n    description: All operations must have at least one tag for grouping in the Batch Actuator API.\n    message: \"Operation '{{property}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  spring-batch-operationid-required:\n    description: All operations in the Spring Batch Actuator API must have an operationId.\n    message: \"OperationId is required for every operation.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n\
  \      field: operationId\n      function: truthy\n\n  spring-batch-operationid-camelcase:\n    description: OperationIds must use camelCase to match Spring Batch conventions.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spring-batch-response-200-required:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation must define a 200 OK response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  spring-batch-schema-description:\n    description: All named schemas should have a description to support batch domain documentation.\n    message: \"Schema '{{property}}' is missing a description.\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field:\
  \ description\n      function: truthy\n\n  spring-batch-status-enum:\n    description: Batch status fields should use the standard Spring Batch status enum values.\n    message: \"Status field should use Spring Batch BatchStatus values.\"\n    severity: info\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n\n  spring-batch-pagination-consistency:\n    description: Paginated responses should include page, size, totalElements, and totalPages.\n    message: \"Paginated response schema should include page, size, totalElements, and totalPages.\"\n    severity: warn\n    given: \"$.components.schemas[?(@.description =~ /[Pp]aginated/)]\"\n    then:\n      field: properties\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - page\n            - size\n            - totalElements\n            - totalPages\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-batch-5-1/refs/heads/main/rules/spring-batch-51-rules.yml
tags:
- Batch Processing
- Data Processing
- Enterprise
- ETL
- Java
- Job Scheduling
- Spring Framework
- Spectral
- Linting
- API Governance
---
