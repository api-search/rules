---
api_specs:
- filename: sonarqube-web-api-openapi.yml
  format: yaml
  label: SonarQube Web API
  slug: web-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sonarqube/refs/heads/main/openapi/sonarqube-web-api-openapi.yml
categories:
- sonarqube
description: Spectral linting rules defining API design standards and conventions for SonarQube.
layout: rules
name: SonarQube API Rules
provider_name: SonarQube
provider_slug: sonarqube
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sonarqube-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sonarqube-operation-id-required
  severity: error
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: sonarqube-tags-required
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get.responses
  name: sonarqube-200-response-for-get
  severity: error
- description: Non-public endpoints must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: sonarqube-security-on-protected-routes
  severity: warn
- description: List/search operations should support pagination parameters
  given: $.paths[*search*].get.parameters[*].name
  name: sonarqube-paging-params-on-list
  severity: info
- description: Successful GET responses should have schemas defined
  given: $.paths[*].get.responses[200].content
  name: sonarqube-response-schema-defined
  severity: warn
- description: SonarQube POST endpoints use form-encoded bodies
  given: $.paths[*].post.requestBody.content
  name: sonarqube-form-encoded-post
  severity: info
- description: Component-scoped endpoints should use 'component' or 'project' parameter
  given: $.paths[*].get.parameters[*].name
  name: sonarqube-component-key-param
  severity: info
rules_file: rules/sonarqube-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sonarqube/refs/heads/main/rules/sonarqube-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 4
slug: sonarqube-rules
source_filename: sonarqube-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sonarqube-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\\s[A-Z][a-z]*)*$\"\n\n  sonarqube-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sonarqube-tags-required:\n    description: All operations must be tagged\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  sonarqube-200-response-for-get:\n    description: All GET operations must define a 200 response\n\
  \    message: GET operation must have a 200 response defined\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  sonarqube-security-on-protected-routes:\n    description: Non-public endpoints must define security requirements\n    message: Protected operation must define security schemes\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  sonarqube-paging-params-on-list:\n    description: List/search operations should support pagination parameters\n    message: Search/list operations should include 'p' and 'ps' pagination parameters\n    severity: info\n    given: \"$.paths[*search*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values: [q, p, ps, filter, f]\n\n  sonarqube-response-schema-defined:\n    description: Successful GET responses should have schemas defined\n    message:\
  \ Response 200 should include a content schema\n    severity: warn\n    given: \"$.paths[*].get.responses[200].content\"\n    then:\n      function: truthy\n\n  sonarqube-form-encoded-post:\n    description: SonarQube POST endpoints use form-encoded bodies\n    message: >-\n      SonarQube API POST endpoints use application/x-www-form-urlencoded,\n      not application/json\n    severity: info\n    given: \"$.paths[*].post.requestBody.content\"\n    then:\n      function: truthy\n\n  sonarqube-component-key-param:\n    description: Component-scoped endpoints should use 'component' or 'project' parameter\n    message: Component-scoped operations should use 'component' or 'project' parameter name\n    severity: info\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values: [component, project, componentKeys, projectKey, key]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sonarqube/refs/heads/main/rules/sonarqube-rules.yml
tags:
- Code Quality
- DevOps
- Security
- Static Analysis
- Spectral
- Linting
- API Governance
---
