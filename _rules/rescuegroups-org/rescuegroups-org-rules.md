---
api_specs:
- filename: rescuegroups-org-openapi.yml
  format: yaml
  label: RescueGroups.org API
  slug: rescuegroups-org
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rescuegroups-org/refs/heads/main/openapi/rescuegroups-org-openapi.yml
categories:
- rescuegroups
description: Spectral linting rules defining API design standards and conventions for RescueGroups.org.
layout: rules
name: RescueGroups.org API Rules
provider_name: RescueGroups.org
provider_slug: rescuegroups-org
rule_count: 11
rules:
- description: All public endpoints must be prefixed with /public/.
  given: $.paths[?(!@property.match(/^\/public\//) && !@property.match(/^\/tokens/))]
  name: rescuegroups-path-prefix
  severity: warn
- description: All RescueGroups.org API operations must use application/vnd.api+json.
  given: $.paths[*][*].responses[*].content
  name: rescuegroups-content-type
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: rescuegroups-operation-id
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: rescuegroups-operation-summary
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: rescuegroups-operation-tags
  severity: warn
- description: Path segments should use kebab-case.
  given: $.paths[*]~
  name: rescuegroups-path-kebab-case
  severity: warn
- description: POST and PATCH operations should document 400 responses.
  given: $.paths[*][post,patch]
  name: rescuegroups-response-400
  severity: warn
- description: All operations should document 401 Unauthorized responses.
  given: $.paths[*][get,post,put,patch,delete]
  name: rescuegroups-response-401
  severity: warn
- description: Responses should reference component schemas following JSON API structure.
  given: $.paths[*][*].responses['200','201'].content['application/vnd.api+json'].schema
  name: rescuegroups-jsonapi-response-schema
  severity: info
- description: GET collection endpoints should support page and limit query parameters.
  given: $.paths[?(!@property.match(/{.*}/) && !@property.match(/search/) && !@property.match(/tokens/))].get
  name: rescuegroups-pagination-params
  severity: info
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: rescuegroups-tags-title-case
  severity: warn
rules_file: rules/rescuegroups-org-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rescuegroups-org/refs/heads/main/rules/rescuegroups-org-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 7
slug: rescuegroups-org-rules
source_filename: rescuegroups-org-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rescuegroups-path-prefix:\n    description: All public endpoints must be prefixed with /public/.\n    message: Public endpoints should use the /public/ path prefix.\n    severity: warn\n    given: $.paths[?(!@property.match(/^\\/public\\//) && !@property.match(/^\\/tokens/))]\n    then:\n      function: falsy\n\n  rescuegroups-content-type:\n    description: All RescueGroups.org API operations must use application/vnd.api+json.\n    message: Operations should accept/produce application/vnd.api+json media type.\n    severity: warn\n    given: $.paths[*][*].responses[*].content\n    then:\n      field: application/vnd.api+json\n      function: truthy\n\n  rescuegroups-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  rescuegroups-operation-summary:\n    description:\
  \ All operations must have a summary.\n    message: Operation is missing a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  rescuegroups-operation-tags:\n    description: All operations must have at least one tag.\n    message: Operation is missing tags.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  rescuegroups-path-kebab-case:\n    description: Path segments should use kebab-case.\n    message: Path segment should use kebab-case.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^(\\/[a-z][a-z0-9-]*(\\{[a-zA-Z_]+\\})?)*$'\n\n  rescuegroups-response-400:\n    description: POST and PATCH operations should document 400 responses.\n    message: POST/PATCH operation should have a 400 response.\n    severity: warn\n    given: $.paths[*][post,patch]\n\
  \    then:\n      field: responses.400\n      function: truthy\n\n  rescuegroups-response-401:\n    description: All operations should document 401 Unauthorized responses.\n    message: Operation should have a 401 response.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses.401\n      function: truthy\n\n  rescuegroups-jsonapi-response-schema:\n    description: Responses should reference component schemas following JSON API structure.\n    message: Response should reference a schema with data property.\n    severity: info\n    given: $.paths[*][*].responses['200','201'].content['application/vnd.api+json'].schema\n    then:\n      function: truthy\n\n  rescuegroups-pagination-params:\n    description: GET collection endpoints should support page and limit query parameters.\n    message: Collection GET endpoint should document pagination parameters.\n    severity: info\n    given: $.paths[?(!@property.match(/{.*}/) && !@property.match(/search/)\
  \ && !@property.match(/tokens/))].get\n    then:\n      field: parameters\n      function: truthy\n\n  rescuegroups-tags-title-case:\n    description: All tags must use Title Case.\n    message: Tag name should use Title Case.\n    severity: warn\n    given: $.tags[*].name\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][A-Za-z ]*$'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rescuegroups-org/refs/heads/main/rules/rescuegroups-org-rules.yml
tags:
- Animals
- Pet Adoption
- Rescue
- Animal Welfare
- Spectral
- Linting
- API Governance
---
