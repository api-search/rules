---
categories:
- rightsline
description: Spectral linting rules defining API design standards and conventions for Rightsline.
layout: rules
name: Rightsline API Rules
provider_name: Rightsline
provider_slug: rightsline
rule_count: 11
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: rightsline-operation-summary-title-case
  severity: warn
- description: Operation IDs should be camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: rightsline-operation-id-camel-case
  severity: warn
- description: Tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: rightsline-tags-title-case
  severity: warn
- description: All operations must require authentication
  given: $.paths[*][get,post,put,patch,delete]
  name: rightsline-must-have-authentication
  severity: error
- description: GET operations must return a 200 response
  given: $.paths[*].get
  name: rightsline-get-must-have-200
  severity: error
- description: POST create operations should return 201 Created
  given: $.paths[*].post
  name: rightsline-post-must-have-201
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: rightsline-delete-must-have-204
  severity: warn
- description: Bulk operation descriptions must note the 100 record limit
  given: $.paths[*].post.description
  name: rightsline-bulk-operations-max-100
  severity: info
- description: Path parameters must be required
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]
  name: rightsline-path-params-required
  severity: error
- description: List endpoints should support limit parameter
  given: $.paths[*].get.parameters[?(@.name == 'limit')]
  name: rightsline-pagination-limit-parameter
  severity: warn
- description: All servers must use HTTPS
  given: $.servers[*].url
  name: rightsline-servers-must-be-https
  severity: error
rules_file: rules/rightsline-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rightsline/refs/heads/main/rules/rightsline-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 6
slug: rightsline-rules
source_filename: rightsline-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rightsline-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-zA-Z]* )*[A-Z][a-zA-Z]*$\"\n\n  rightsline-operation-id-camel-case:\n    description: Operation IDs should be camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rightsline-tags-title-case:\n    description: Tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  rightsline-must-have-authentication:\n    description: All operations must require authentication\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: security\n      function: defined\n\n  rightsline-get-must-have-200:\n    description: GET operations must return a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  rightsline-post-must-have-201:\n    description: POST create operations should return 201 Created\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.201\n      function: defined\n\n  rightsline-delete-must-have-204:\n    description: DELETE operations should return 204 No Content\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: defined\n\n  rightsline-bulk-operations-max-100:\n    description: Bulk operation descriptions must note the 100 record limit\n    severity: info\n    given: \"$.paths[*].post.description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"100\"\n\n  rightsline-path-params-required:\n\
  \    description: Path parameters must be required\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  rightsline-pagination-limit-parameter:\n    description: List endpoints should support limit parameter\n    severity: warn\n    given: \"$.paths[*].get.parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema.maximum\n      function: defined\n\n  rightsline-servers-must-be-https:\n    description: All servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rightsline/refs/heads/main/rules/rightsline-rules.yml
tags:
- Content Management
- Entertainment
- Media
- Rights Management
- Royalties
- Spectral
- Linting
- API Governance
---
