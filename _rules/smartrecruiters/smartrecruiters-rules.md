---
api_specs:
- filename: smartrecruiters-posting-openapi.yml
  format: yaml
  label: SmartRecruiters Posting API
  slug: posting-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smartrecruiters/refs/heads/main/openapi/smartrecruiters-posting-openapi.yml
- filename: smartrecruiters-jobs-openapi.yml
  format: yaml
  label: SmartRecruiters Job API
  slug: job-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smartrecruiters/refs/heads/main/openapi/smartrecruiters-jobs-openapi.yml
- filename: smartrecruiters-candidates-openapi.yml
  format: yaml
  label: SmartRecruiters Candidate API
  slug: candidate-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smartrecruiters/refs/heads/main/openapi/smartrecruiters-candidates-openapi.yml
categories:
- smartrecruiters
description: Spectral linting rules defining API design standards and conventions for SmartRecruiters.
layout: rules
name: SmartRecruiters API Rules
provider_name: SmartRecruiters
provider_slug: smartrecruiters
rule_count: 10
rules:
- description: All operations must have at least one tag for grouping
  given: $.paths[*][*]
  name: smartrecruiters-operation-tags
  severity: warn
- description: All operations must have an operationId in camelCase
  given: $.paths[*][*]
  name: smartrecruiters-operation-ids
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smartrecruiters-summary-title-case
  severity: warn
- description: List operations should support limit and offset pagination parameters
  given: $.paths[*].get
  name: smartrecruiters-pagination-params
  severity: warn
- description: List endpoints should return a ListResult wrapper with limit, offset, totalFound, and content fields
  given: $.paths[*].get.responses.200.content['application/json'].schema
  name: smartrecruiters-list-result-wrapper
  severity: warn
- description: Paths that access company-scoped resources must include companyIdentifier path parameter
  given: $.paths['/v1/companies/{companyIdentifier}/*']
  name: smartrecruiters-company-identifier-path
  severity: warn
- description: All operations must define 401 and 403 error responses
  given: $.paths[*][post,put,patch,delete]
  name: smartrecruiters-error-responses
  severity: error
- description: Request bodies must use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: smartrecruiters-content-type
  severity: error
- description: API must define authentication security schemes (ApiKey or OAuth2)
  given: $.components.securitySchemes
  name: smartrecruiters-security-scheme
  severity: error
- description: API paths must not have trailing slashes
  given: $.paths
  name: smartrecruiters-no-trailing-slashes
  severity: warn
rules_file: rules/smartrecruiters-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smartrecruiters/refs/heads/main/rules/smartrecruiters-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: smartrecruiters-rules
source_filename: smartrecruiters-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  smartrecruiters-operation-tags:\n    description: All operations must have at least one tag for grouping\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smartrecruiters-operation-ids:\n    description: All operations must have an operationId in camelCase\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  smartrecruiters-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  smartrecruiters-pagination-params:\n    description: List operations should support limit and offset pagination parameters\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type:\
  \ object\n          properties:\n            parameters:\n              type: array\n              contains:\n                type: object\n                properties:\n                  name:\n                    enum: [limit, offset]\n\n  smartrecruiters-list-result-wrapper:\n    description: >-\n      List endpoints should return a ListResult wrapper with limit, offset,\n      totalFound, and content fields\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            '$ref':\n              type: string\n\n  smartrecruiters-company-identifier-path:\n    description: >-\n      Paths that access company-scoped resources must include companyIdentifier\n      path parameter\n    severity: warn\n    given: \"$.paths['/v1/companies/{companyIdentifier}/*']\"\n    then:\n      function: truthy\n\n  smartrecruiters-error-responses:\n\
  \    description: All operations must define 401 and 403 error responses\n    severity: error\n    given: \"$.paths[*][post,put,patch,delete]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '401'\n            - '403'\n\n  smartrecruiters-content-type:\n    description: Request bodies must use application/json content type\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - 'application/json'\n\n  smartrecruiters-security-scheme:\n    description: API must define authentication security schemes (ApiKey or OAuth2)\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  smartrecruiters-no-trailing-slashes:\n    description: API paths must not have trailing slashes\n\
  \    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smartrecruiters/refs/heads/main/rules/smartrecruiters-rules.yml
tags:
- Human Resources
- Recruiting
- Talent Acquisition
- Applicant Tracking
- HR Technology
- Spectral
- Linting
- API Governance
---
