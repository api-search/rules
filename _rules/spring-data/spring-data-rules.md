---
api_specs:
- filename: spring-data-rest-openapi.yml
  format: yaml
  label: Spring Data REST
  slug: spring-data-rest
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-data/refs/heads/main/openapi/spring-data-rest-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Data.
layout: rules
name: Spring Data API Rules
provider_name: Spring Data
provider_slug: spring-data
rule_count: 7
rules:
- description: Spring Data REST endpoints should accept/produce application/hal+json
  given: $.paths[*][*].responses[*].content
  name: spring-data-hal-content-type
  severity: warn
- description: Collection endpoints should support page, size, and sort query parameters
  given: $.paths[*].get
  name: spring-data-pageable-parameters
  severity: info
- description: All operations must have a unique operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-data-rest-operation-ids
  severity: error
- description: Operations must include at least one tag using Title Case
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-data-rest-tags
  severity: warn
- description: API paths must not have trailing slashes
  given: $.paths
  name: spring-data-no-trailing-slashes
  severity: warn
- description: Resource schemas should include _links property for HATEOAS compliance
  given: $.components.schemas[*]
  name: spring-data-hateoas-links
  severity: info
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spring-data-rest-summaries-title-case
  severity: warn
rules_file: rules/spring-data-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-data/refs/heads/main/rules/spring-data-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 4
slug: spring-data-rules
source_filename: spring-data-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-data-hal-content-type:\n    description: Spring Data REST endpoints should accept/produce application/hal+json\n    message: \"{{description}}. Found: {{value}}\"\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      field: \"application/hal+json\"\n      function: truthy\n\n  spring-data-pageable-parameters:\n    description: Collection endpoints should support page, size, and sort query parameters\n    message: \"Collection GET operations should include page, size, and sort parameters\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  spring-data-rest-operation-ids:\n    description: All operations must have a unique operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n  \
  \    function: truthy\n\n  spring-data-rest-tags:\n    description: Operations must include at least one tag using Title Case\n    message: \"Operation must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spring-data-no-trailing-slashes:\n    description: API paths must not have trailing slashes\n    message: \"Path {{path}} has a trailing slash\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  spring-data-hateoas-links:\n    description: Resource schemas should include _links property for HATEOAS compliance\n    message: \"Resource schemas should define _links property\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  spring-data-rest-summaries-title-case:\n    description: Operation summaries\
  \ must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-data/refs/heads/main/rules/spring-data-rules.yml
tags:
- Data Access
- Database
- Framework
- Java
- JPA
- MongoDB
- ORM
- Redis
- REST
- Spring
- Spectral
- Linting
- API Governance
---
