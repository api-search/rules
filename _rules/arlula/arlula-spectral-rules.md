---
categories:
- arlula
description: Spectral linting rules defining API design standards and conventions for Arlula.
layout: rules
name: Arlula API Rules
provider_name: Arlula
provider_slug: arlula
rule_count: 30
rules:
- description: API must have a title.
  given: $.info
  name: arlula-info-title
  severity: error
- description: API must have a description.
  given: $.info
  name: arlula-info-description
  severity: warn
- description: API must have a version.
  given: $.info
  name: arlula-info-version
  severity: error
- description: API should have contact information.
  given: $.info
  name: arlula-info-contact
  severity: warn
- description: Must use OpenAPI 3.0.x.
  given: $
  name: arlula-openapi-version
  severity: error
- description: API must have servers defined.
  given: $
  name: arlula-servers-present
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: arlula-servers-https
  severity: error
- description: API must have paths defined.
  given: $
  name: arlula-paths-present
  severity: error
- description: Path segments should use kebab-case or camelCase consistently.
  given: $.paths[*]~
  name: arlula-path-kebab-case
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: arlula-operation-summary
  severity: error
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: arlula-operation-description
  severity: warn
- description: Every operation must have tags.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: arlula-operation-tags
  severity: error
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: arlula-operation-id
  severity: error
- description: Parameters should have descriptions.
  given: $.paths[*][get,post,put,patch,delete][parameters][*]
  name: arlula-parameter-description
  severity: warn
- description: Parameters must have a schema.
  given: $.paths[*][get,post,put,patch,delete][parameters][*]
  name: arlula-parameter-schema
  severity: error
- description: Request bodies must have content defined.
  given: $.paths[*][post,put,patch].requestBody
  name: arlula-request-body-content
  severity: error
- description: POST/PUT/PATCH operations should accept application/json.
  given: $.paths[*][post,put,patch].requestBody.content
  name: arlula-request-body-json
  severity: warn
- description: GET operations should define a 200 response.
  given: $.paths[*].get.responses
  name: arlula-response-200
  severity: warn
- description: Responses must have descriptions.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: arlula-response-description
  severity: error
- description: Operations should document 401 Unauthorized responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: arlula-response-401
  severity: warn
- description: Operations should document 500 error responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: arlula-response-500
  severity: warn
- description: Schemas in components should have titles.
  given: $.components.schemas[*]
  name: arlula-schema-title
  severity: warn
- description: Schemas should have descriptions.
  given: $.components.schemas[*]
  name: arlula-schema-description
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: arlula-property-description
  severity: warn
- description: Schema properties should have examples.
  given: $.components.schemas[*].properties[*]
  name: arlula-property-example
  severity: info
- description: API must define security schemes.
  given: $.components
  name: arlula-security-defined
  severity: error
- description: Arlula API uses HTTP Basic authentication.
  given: $.components.securitySchemes.BasicAuth
  name: arlula-security-basic-auth
  severity: error
- description: Archive search must use POST method.
  given: $.paths['/api/archive/search']
  name: arlula-archive-search-post
  severity: warn
- description: Tasking search must use POST method.
  given: $.paths['/api/tasking/search']
  name: arlula-tasking-search-post
  severity: warn
- description: Resource data download should support binary responses.
  given: $.paths['/api/resource/{resource}/data'].get.responses['200'].content
  name: arlula-resource-data-binary
  severity: info
rules_file: rules/arlula-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/arlula/refs/heads/main/rules/arlula-spectral-rules.yml
severity_counts:
  error: 14
  hint: 0
  info: 2
  warn: 14
slug: arlula-spectral-rules
tags:
- Earth Observation
- Geospatial
- Imagery
- Remote Sensing
- Satellites
- Spectral
- Linting
- API Governance
---
