---
api_specs:
- filename: spring-initializr-openapi.yml
  format: yaml
  label: Spring Initializr API
  slug: spring-initializr
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-framework/refs/heads/main/openapi/spring-initializr-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Framework.
layout: rules
name: Spring Framework API Rules
provider_name: Spring Framework
provider_slug: spring-framework
rule_count: 6
rules:
- description: All operations must have a unique operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-framework-operation-id-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-framework-tags-required
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spring-framework-summary-title-case
  severity: warn
- description: Servers should define a base URL
  given: $
  name: spring-framework-api-versioning
  severity: warn
- description: GET operations should have a 200 response
  given: $.paths[*].get
  name: spring-framework-response-200
  severity: error
- description: Operations and parameters should have descriptions
  given: $.paths[*][*]
  name: spring-framework-no-empty-descriptions
  severity: info
rules_file: rules/spring-framework-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-framework/refs/heads/main/rules/spring-framework-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 3
slug: spring-framework-rules
source_filename: spring-framework-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-framework-operation-id-required:\n    description: All operations must have a unique operationId\n    message: \"Operation is missing operationId at {{path}}\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spring-framework-tags-required:\n    description: All operations must have tags\n    message: \"Operation at {{path}} is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spring-framework-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should begin with an uppercase letter\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-framework-api-versioning:\n    description: Servers\
  \ should define a base URL\n    message: \"API should define at least one server\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  spring-framework-response-200:\n    description: GET operations should have a 200 response\n    message: \"GET operation at {{path}} is missing a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: \"responses.200\"\n      function: truthy\n\n  spring-framework-no-empty-descriptions:\n    description: Operations and parameters should have descriptions\n    message: \"Description is required at {{path}}\"\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-framework/refs/heads/main/rules/spring-framework-rules.yml
tags:
- AOP
- Dependency Injection
- Enterprise
- Framework
- IoC
- Java
- Microservices
- MVC
- Spring Boot
- Spectral
- Linting
- API Governance
---
