---
api_specs:
- filename: weaviate-openapi.yml
  format: yaml
  label: Weaviate REST API
  slug: weaviate-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/weaviate/refs/heads/main/openapi/weaviate-openapi.yml
categories:
- weaviate
description: Spectral linting rules defining API design standards and conventions for Weaviate.
layout: rules
name: Weaviate API Rules
provider_name: Weaviate
provider_slug: weaviate
rule_count: 22
rules:
- description: Weaviate API specs must use OpenAPI 3.0.x
  given: $
  name: weaviate-openapi-version
  severity: error
- description: API must have a title
  given: $.info
  name: weaviate-info-title
  severity: error
- description: API must have a description
  given: $.info
  name: weaviate-info-description
  severity: warn
- description: API must have a version
  given: $.info
  name: weaviate-info-version
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch,head,options]
  name: weaviate-operation-summary
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch,head,options]
  name: weaviate-operation-description
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch,head,options]
  name: weaviate-operation-operationid
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,delete,patch,head,options]
  name: weaviate-operation-tags
  severity: warn
- description: All operations must have responses
  given: $.paths[*][get,post,put,delete,patch,head,options]
  name: weaviate-operation-responses
  severity: error
- description: GET and POST operations should have a 200 response
  given: $.paths[*][get,post]
  name: weaviate-response-200
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: weaviate-schema-properties-description
  severity: info
- description: Path segments should use kebab-case
  given: $.paths
  name: weaviate-path-kebab-case
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: weaviate-parameter-description
  severity: warn
- description: Request bodies must define content
  given: $.paths[*][post,put,patch].requestBody
  name: weaviate-request-body-content
  severity: error
- description: API must define security schemes
  given: $.components
  name: weaviate-security-schemes
  severity: warn
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: weaviate-operation-id-camel-case
  severity: info
- description: Schema objects should have a type defined
  given: $.components.schemas[*]
  name: weaviate-schema-type
  severity: info
- description: Path items must have at least one operation
  given: $.paths[*]
  name: weaviate-no-empty-paths
  severity: error
- description: Vector database operations should be tagged appropriately
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: weaviate-vector-db-tags
  severity: info
- description: Object IDs should use UUID format
  given: $.components.schemas[*].properties.id
  name: weaviate-uuid-format
  severity: info
- description: Operations should have Microcks extensions for testing
  given: $.paths[*][get,post,put,delete,patch]
  name: weaviate-microcks-operation
  severity: info
- description: API must define servers
  given: $
  name: weaviate-servers-defined
  severity: error
rules_file: rules/weaviate-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/weaviate/refs/heads/main/rules/weaviate-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 8
  warn: 6
slug: weaviate-spectral-rules
source_filename: weaviate-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  weaviate-openapi-version:\n    description: Weaviate API specs must use OpenAPI 3.0.x\n    message: \"OpenAPI version must be 3.0.x\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  weaviate-info-title:\n    description: API must have a title\n    message: \"Info object must have a title\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  weaviate-info-description:\n    description: API must have a description\n    message: \"Info object must have a description\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  weaviate-info-version:\n    description: API must have a version\n    message: \"Info object must have a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  weaviate-operation-summary:\n\
  \    description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch,head,options]\"\n    then:\n      field: summary\n      function: truthy\n\n  weaviate-operation-description:\n    description: All operations should have a description\n    message: \"Operation should have a description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch,head,options]\"\n    then:\n      field: description\n      function: truthy\n\n  weaviate-operation-operationid:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  weaviate-operation-tags:\n    description: All operations must have tags\n    message: \"Operation must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch,head,options]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  weaviate-operation-responses:\n    description: All operations must have responses\n    message: \"Operation must have responses defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch,head,options]\"\n    then:\n      field: responses\n      function: truthy\n\n  weaviate-response-200:\n    description: GET and POST operations should have a 200 response\n    message: \"GET/POST operations should define a 200 response\"\n    severity: warn\n    given: \"$.paths[*][get,post]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  weaviate-schema-properties-description:\n    description: Schema properties should have descriptions\n    message: \"Schema properties should have descriptions\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  weaviate-path-kebab-case:\n    description: Path segments should\
  \ use kebab-case\n    message: \"Path segments should use kebab-case (lowercase with hyphens)\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+/?$\"\n\n  weaviate-parameter-description:\n    description: Parameters should have descriptions\n    message: \"Parameter should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  weaviate-request-body-content:\n    description: Request bodies must define content\n    message: \"Request body must have content defined\"\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: content\n      function: truthy\n\n  weaviate-security-schemes:\n    description: API must define security schemes\n    message: \"Security schemes must be defined in components\"\n    severity: warn\n    given: \"$.components\"\
  \n    then:\n      field: securitySchemes\n      function: truthy\n\n  weaviate-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId should use camelCase naming\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  weaviate-schema-type:\n    description: Schema objects should have a type defined\n    message: \"Schema should define a type\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [type]\n            - required: [allOf]\n            - required: [anyOf]\n            - required: [oneOf]\n\n  weaviate-no-empty-paths:\n    description: Path items must have at least one operation\n    message: \"Path item must have at least one HTTP method defined\"\n    severity: error\n\
  \    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          minProperties: 1\n\n  weaviate-vector-db-tags:\n    description: Vector database operations should be tagged appropriately\n    message: \"Operations should use standard Weaviate tags\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - objects\n          - schema\n          - backups\n          - batch\n          - graphql\n          - nodes\n          - oidc\n          - authz\n          - users\n          - replication\n          - tenants\n          - classifications\n          - aliases\n          - namespaces\n          - cluster\n          - mcp\n          - well-known\n\n  weaviate-uuid-format:\n    description: Object IDs should use UUID format\n    message: \"ID properties should use UUID format\"\n    severity: info\n    given: \"$.components.schemas[*].properties.id\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            format:\n              enum: [uuid]\n\n  weaviate-microcks-operation:\n    description: Operations should have Microcks extensions for testing\n    message: \"Operation should include x-microcks-operation extension\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  weaviate-servers-defined:\n    description: API must define servers\n    message: \"Servers array must be defined\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/weaviate/refs/heads/main/rules/weaviate-spectral-rules.yml
tags:
- Vector Database
- AI
- Machine Learning
- Semantic Search
- Open Source
- GraphQL
- Kubernetes
- Spectral
- Linting
- API Governance
---
