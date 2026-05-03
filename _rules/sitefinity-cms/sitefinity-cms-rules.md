---
api_specs:
- filename: sitefinity-cms-content-api-openapi.yml
  format: yaml
  label: Sitefinity CMS Content API
  slug: content-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitefinity-cms/refs/heads/main/openapi/sitefinity-cms-content-api-openapi.yml
categories:
- sitefinity
description: Spectral linting rules defining API design standards and conventions for Sitefinity CMS.
layout: rules
name: Sitefinity CMS API Rules
provider_name: Sitefinity CMS
provider_slug: sitefinity-cms
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sitefinity-operation-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: sitefinity-operation-id-camel-case
  severity: error
- description: List responses should use OData value wrapper with @odata.count
  given: $.paths[*].get.responses['200'].content['application/json'].schema
  name: sitefinity-odata-collection-response
  severity: info
- description: Sitefinity CMS uses cookie-based ASP.NET authentication
  given: $.components.securitySchemes
  name: sitefinity-cookie-auth-scheme
  severity: info
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: sitefinity-delete-returns-204
  severity: warn
- description: POST operations must include a request body
  given: $.paths[*].post
  name: sitefinity-post-has-request-body
  severity: error
- description: Schema model names should use PascalCase (Sitefinity .NET convention)
  given: $.components.schemas
  name: sitefinity-pascal-case-model-names
  severity: info
- description: API must define at least one server
  given: $
  name: sitefinity-servers-defined
  severity: error
- description: Info section must include contact details
  given: $.info
  name: sitefinity-info-contact
  severity: warn
- description: Root tags must be defined for all operation tags
  given: $.tags
  name: sitefinity-tags-defined
  severity: warn
rules_file: rules/sitefinity-cms-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sitefinity-cms/refs/heads/main/rules/sitefinity-cms-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 3
  warn: 4
slug: sitefinity-cms-rules
source_filename: sitefinity-cms-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sitefinity-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z\\\\s]*$\"\n\n  sitefinity-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sitefinity-odata-collection-response:\n    description: List responses should use OData value wrapper with @odata.count\n    severity: info\n    given: \"$.paths[*].get.responses['200'].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  sitefinity-cookie-auth-scheme:\n    description: Sitefinity CMS uses cookie-based ASP.NET authentication\n\
  \    severity: info\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  sitefinity-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  sitefinity-post-has-request-body:\n    description: POST operations must include a request body\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  sitefinity-pascal-case-model-names:\n    description: Schema model names should use PascalCase (Sitefinity .NET convention)\n    severity: info\n    given: \"$.components.schemas\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  sitefinity-servers-defined:\n    description: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\
  \n  sitefinity-info-contact:\n    description: Info section must include contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sitefinity-tags-defined:\n    description: Root tags must be defined for all operation tags\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sitefinity-cms/refs/heads/main/rules/sitefinity-cms-rules.yml
tags:
- Content Management
- Headless CMS
- .NET
- REST
- Spectral
- Linting
- API Governance
---
