---
api_specs:
- filename: sourceforge-allura-openapi.yml
  format: yaml
  label: SourceForge Allura API
  slug: sourceforge-allura-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sourceforge/refs/heads/main/openapi/sourceforge-allura-openapi.yml
categories:
- sourceforge
description: Spectral linting rules defining API design standards and conventions for SourceForge.
layout: rules
name: SourceForge API Rules
provider_name: SourceForge
provider_slug: sourceforge
rule_count: 12
rules:
- description: All SourceForge API paths must begin with /rest/
  given: $.paths
  name: sourceforge-rest-prefix
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sourceforge-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sourceforge-operation-id-required
  severity: error
- description: OperationId must use camelCase convention
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sourceforge-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sourceforge-operation-has-tags
  severity: warn
- description: POST operations must define a requestBody
  given: $.paths[*].post
  name: sourceforge-post-has-request-body
  severity: error
- description: Operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sourceforge-401-response
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: sourceforge-delete-returns-204
  severity: warn
- description: All tags in the spec must use Title Case
  given: $.tags[*].name
  name: sourceforge-tags-title-case
  severity: warn
- description: OAuth2 security must be defined globally or per operation
  given: $
  name: sourceforge-security-defined
  severity: error
- description: Project-scoped paths must use {project} path parameter
  given: $.paths['/rest/p/{project}']
  name: sourceforge-project-parameter
  severity: info
- description: Successful responses must have a schema
  given: $.paths[*][get,post].responses['200','201'].content['application/json']
  name: sourceforge-response-schema-defined
  severity: warn
rules_file: rules/sourceforge-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sourceforge/refs/heads/main/rules/sourceforge-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 7
slug: sourceforge-rules
source_filename: sourceforge-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # SourceForge uses /rest/ prefix for all endpoints\n  sourceforge-rest-prefix:\n    description: All SourceForge API paths must begin with /rest/\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/rest\\\\/\"\n\n  # All operations must have summaries in Title Case\n  sourceforge-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # All operations must have operationId\n  sourceforge-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId must use\
  \ camelCase\n  sourceforge-operation-id-camel-case:\n    description: OperationId must use camelCase convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have tags\n  sourceforge-operation-has-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # POST operations should have requestBody\n  sourceforge-post-has-request-body:\n    description: POST operations must define a requestBody\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # 401 response required\n  sourceforge-401-response:\n    description: Operations must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    then:\n      field: \"401\"\n      function: defined\n\n  # DELETE returns 204\n  sourceforge-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: defined\n\n  # All tags must be Title Case\n  sourceforge-tags-title-case:\n    description: All tags in the spec must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # Security must be defined\n  sourceforge-security-defined:\n    description: OAuth2 security must be defined globally or per operation\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: defined\n\n  # Project path parameter must exist for project-scoped operations\n  sourceforge-project-parameter:\n    description: Project-scoped paths must use {project}\
  \ path parameter\n    severity: info\n    given: \"$.paths['/rest/p/{project}']\"\n    then:\n      function: defined\n\n  # Response schemas must be defined\n  sourceforge-response-schema-defined:\n    description: Successful responses must have a schema\n    severity: warn\n    given: \"$.paths[*][get,post].responses['200','201'].content['application/json']\"\n    then:\n      field: schema\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sourceforge/refs/heads/main/rules/sourceforge-rules.yml
tags:
- Open Source
- Developer Tools
- Project Management
- Code Hosting
- Collaboration
- Spectral
- Linting
- API Governance
---
