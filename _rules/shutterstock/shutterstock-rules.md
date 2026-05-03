---
api_specs:
- filename: shutterstock-openapi.yml
  format: yaml
  label: Shutterstock API
  slug: shutterstock-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shutterstock/refs/heads/main/openapi/shutterstock-openapi.yml
categories:
- shutterstock
description: Spectral linting rules defining API design standards and conventions for Shutterstock.
layout: rules
name: Shutterstock API Rules
provider_name: Shutterstock
provider_slug: shutterstock
rule_count: 10
rules:
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: shutterstock-operation-tags
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: shutterstock-operation-summary
  severity: error
- description: All API paths must begin with /v2
  given: $.paths
  name: shutterstock-v2-path-prefix
  severity: error
- description: All GET operations must have a 200 response
  given: $.paths[*].get.responses
  name: shutterstock-response-200
  severity: error
- description: The API must define OAuth 2.0 security scheme
  given: $.components.securitySchemes
  name: shutterstock-oauth-security
  severity: error
- description: Search endpoints must have a query parameter
  given: $.paths[?(@property.includes('search'))].get.parameters[?(@.name == 'query')]
  name: shutterstock-search-query-param
  severity: warn
- description: License endpoints must use POST method
  given: $.paths[?(@property.includes('licenses'))].post
  name: shutterstock-license-operation
  severity: warn
- description: Collection endpoints should follow consistent naming
  given: $.paths[?(@property.includes('collections'))][*]
  name: shutterstock-collection-naming
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: shutterstock-operation-id
  severity: error
- description: List endpoints should support pagination
  given: $.paths[*].get.parameters
  name: shutterstock-page-parameter
  severity: info
rules_file: rules/shutterstock-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shutterstock/refs/heads/main/rules/shutterstock-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 3
slug: shutterstock-rules
source_filename: shutterstock-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  shutterstock-operation-tags:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  shutterstock-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: summary\n      function: truthy\n\n  shutterstock-v2-path-prefix:\n    description: All API paths must begin with /v2\n    message: \"API paths must use /v2 prefix\"\n    given: \"$.paths\"\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2\"\n\n  shutterstock-response-200:\n    description: All GET operations must have a 200 response\n    message: \"GET operation must define a 200 response\"\n    given: \"$.paths[*].get.responses\"\n\
  \    severity: error\n    then:\n      field: \"200\"\n      function: truthy\n\n  shutterstock-oauth-security:\n    description: The API must define OAuth 2.0 security scheme\n    message: \"API must include OAuth 2.0 security scheme definition\"\n    given: \"$.components.securitySchemes\"\n    severity: error\n    then:\n      function: defined\n\n  shutterstock-search-query-param:\n    description: Search endpoints must have a query parameter\n    message: \"Search endpoints should include a search query parameter\"\n    given: \"$.paths[?(@property.includes('search'))].get.parameters[?(@.name == 'query')]\"\n    severity: warn\n    then:\n      field: required\n      function: defined\n\n  shutterstock-license-operation:\n    description: License endpoints must use POST method\n    message: \"Licensing operations should use POST\"\n    given: \"$.paths[?(@property.includes('licenses'))].post\"\n    severity: warn\n    then:\n      field: operationId\n      function: truthy\n\n  shutterstock-collection-naming:\n\
  \    description: Collection endpoints should follow consistent naming\n    message: \"Collection operations should be documented consistently\"\n    given: \"$.paths[?(@property.includes('collections'))][*]\"\n    severity: warn\n    then:\n      field: summary\n      function: truthy\n\n  shutterstock-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  shutterstock-page-parameter:\n    description: List endpoints should support pagination\n    message: \"List endpoints should document page or per_page parameters\"\n    given: \"$.paths[*].get.parameters\"\n    severity: info\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shutterstock/refs/heads/main/rules/shutterstock-rules.yml
tags:
- Images
- Media
- Photos
- Stock Images
- Videos
- Audio
- Licensing
- Creative Content
- Spectral
- Linting
- API Governance
---
