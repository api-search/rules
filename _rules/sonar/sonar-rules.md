---
api_specs:
- filename: sonar-sonarcloud-api-openapi.yml
  format: yaml
  label: SonarCloud API
  slug: sonarcloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sonar/refs/heads/main/openapi/sonar-sonarcloud-api-openapi.yml
categories:
- sonar
description: Spectral linting rules defining API design standards and conventions for Sonar.
layout: rules
name: Sonar API Rules
provider_name: Sonar
provider_slug: sonar
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sonar-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sonar-operation-id-required
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: sonar-tags-required
  severity: warn
- description: SonarCloud organization-scoped endpoints should include organization parameter
  given: $.paths[*].get.parameters[*].name
  name: sonar-organization-param-required
  severity: info
- description: GET operations must define 200 response
  given: $.paths[*].get.responses
  name: sonar-200-get-response
  severity: error
- description: All protected endpoints must use bearerAuth security scheme
  given: $.paths[*][get,post,put,patch,delete]
  name: sonar-bearer-auth
  severity: warn
- description: Successful GET responses must include schemas
  given: $.paths[*].get.responses[200].content
  name: sonar-response-schema
  severity: warn
- description: Search/list endpoints should support standard p and ps pagination
  given: $.paths[*search*].get.parameters[*].name
  name: sonar-pagination-support
  severity: info
rules_file: rules/sonar-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sonar/refs/heads/main/rules/sonar-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: sonar-rules
source_filename: sonar-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sonar-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\\s[A-Z][a-z]*)*$\"\n\n  sonar-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sonar-tags-required:\n    description: All operations must have tags\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  sonar-organization-param-required:\n    description: SonarCloud organization-scoped endpoints should include\
  \ organization parameter\n    message: Organization-scoped endpoints should include an 'organization' parameter\n    severity: info\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values: [organization, organizationKey, project, component, componentKeys, q, p, ps, branch, pullRequest]\n\n  sonar-200-get-response:\n    description: GET operations must define 200 response\n    message: GET operation must have a 200 response\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  sonar-bearer-auth:\n    description: All protected endpoints must use bearerAuth security scheme\n    message: Protected operation should define bearerAuth security\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  sonar-response-schema:\n    description: Successful GET responses must include\
  \ schemas\n    message: Response 200 must include a content schema\n    severity: warn\n    given: \"$.paths[*].get.responses[200].content\"\n    then:\n      function: truthy\n\n  sonar-pagination-support:\n    description: Search/list endpoints should support standard p and ps pagination\n    message: Search endpoints should include 'p' and 'ps' query parameters\n    severity: info\n    given: \"$.paths[*search*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values: [q, p, ps, organization, filter]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sonar/refs/heads/main/rules/sonar-rules.yml
tags:
- CI/CD
- Code Quality
- DevOps
- Security
- SonarCloud
- SonarQube
- Static Analysis
- Spectral
- Linting
- API Governance
---
