---
api_specs:
- filename: strapi-rest-api-openapi.yml
  format: yaml
  label: Strapi REST API
  slug: strapi-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-rest-api-openapi.yml
- filename: strapi-admin-panel-api-openapi.yml
  format: yaml
  label: Strapi Admin Panel API
  slug: strapi-admin-panel-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-admin-panel-api-openapi.yml
- filename: strapi-users-and-permissions-api-openapi.yml
  format: yaml
  label: Strapi Users and Permissions API
  slug: strapi-users-permissions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/openapi/strapi-users-and-permissions-api-openapi.yml
- filename: strapi-webhooks-asyncapi.yml
  format: yaml
  label: Strapi Webhooks
  slug: strapi-webhooks
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/asyncapi/strapi-webhooks-asyncapi.yml
categories:
- strapi
description: Spectral linting rules defining API design standards and conventions for Strapi.
layout: rules
name: Strapi API Rules
provider_name: Strapi
provider_slug: strapi
rule_count: 10
rules:
- description: Strapi operationIds use camelCase (e.g., findEntries, createEntry, listAdminUsers). All operation IDs must follow camelCase convention.
  given: $.paths[*][*].operationId
  name: strapi-operation-ids-camel-case
  severity: warn
- description: All OpenAPI tags must use Title Case (e.g., 'Content Entries', 'Admin Users', 'API Tokens').
  given: $.tags[*].name
  name: strapi-tags-title-case
  severity: warn
- description: All content API paths must begin with /api/. Admin API paths must begin with /admin/. Strapi enforces this routing convention.
  given: $.paths
  name: strapi-api-paths-prefix
  severity: warn
- description: Protected Strapi endpoints must declare security using bearerAuth or adminBearerAuth schemes. Public endpoints explicitly set security to [].
  given: $.paths[*][get,put,delete,patch]
  name: strapi-bearer-auth-on-protected-endpoints
  severity: info
- description: Strapi REST API list responses wrap results in a 'data' array with a 'meta' object containing pagination. Single-entry responses wrap the entry in a 'data' object.
  given: $.paths[*][get].responses['200'].content['application/json'].schema.properties
  name: strapi-response-data-wrapper
  severity: info
- description: Strapi v5 uses 'documentId' as the path parameter for content entry identifiers. Path parameters for individual entries must be named 'documentId' (not 'id') in REST API paths.
  given: $.paths['/api/{pluralApiId}/{documentId}'][*].parameters[*]
  name: strapi-document-id-param-name
  severity: info
- description: Strapi list endpoints support both page-based (pagination[page] / pagination[pageSize]) and offset-based (pagination[start] / pagination[limit]) pagination. Both styles use bracket notation.
  given: $.paths[*][get].parameters[*].name
  name: strapi-pagination-parameters
  severity: info
- description: Strapi error responses follow a consistent shape with a top-level 'data' (null) property and an 'error' object containing 'status', 'name', 'message', and 'details'.
  given: $.components.schemas.Error.properties
  name: strapi-error-schema-shape
  severity: warn
- description: All operations must have a summary. Strapi docs use action-noun format (e.g., 'List content entries', 'Create a content entry').
  given: $.paths[*][get,post,put,delete,patch]
  name: strapi-operation-summaries-present
  severity: error
- description: Strapi file upload endpoints must use multipart/form-data content type.
  given: $.paths['/api/upload'][post].requestBody.content
  name: strapi-upload-multipart
  severity: warn
rules_file: rules/strapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/rules/strapi-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 4
  warn: 5
slug: strapi-rules
source_filename: strapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  strapi-operation-ids-camel-case:\n    description: >-\n      Strapi operationIds use camelCase (e.g., findEntries, createEntry,\n      listAdminUsers). All operation IDs must follow camelCase convention.\n    message: \"OperationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  strapi-tags-title-case:\n    description: >-\n      All OpenAPI tags must use Title Case (e.g., 'Content Entries',\n      'Admin Users', 'API Tokens').\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  strapi-api-paths-prefix:\n    description: >-\n      All content API paths must begin with /api/. Admin API paths must\n      begin\
  \ with /admin/. Strapi enforces this routing convention.\n    message: \"Path '{{property}}' must start with /api/ or /admin/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/(api|admin)/\"\n\n  strapi-bearer-auth-on-protected-endpoints:\n    description: >-\n      Protected Strapi endpoints must declare security using bearerAuth or\n      adminBearerAuth schemes. Public endpoints explicitly set security to [].\n    message: \"Protected operation must declare bearerAuth or adminBearerAuth security\"\n    severity: info\n    given: \"$.paths[*][get,put,delete,patch]\"\n    then:\n      function: truthy\n      field: \"security\"\n\n  strapi-response-data-wrapper:\n    description: >-\n      Strapi REST API list responses wrap results in a 'data' array with a\n      'meta' object containing pagination. Single-entry responses wrap the\n      entry in a 'data' object.\n    message: \"200 response\
  \ should include a 'data' property at the top level\"\n    severity: info\n    given: \"$.paths[*][get].responses['200'].content['application/json'].schema.properties\"\n    then:\n      function: truthy\n      field: \"data\"\n\n  strapi-document-id-param-name:\n    description: >-\n      Strapi v5 uses 'documentId' as the path parameter for content entry\n      identifiers. Path parameters for individual entries must be named\n      'documentId' (not 'id') in REST API paths.\n    message: \"Content entry path parameter should be named 'documentId'\"\n    severity: info\n    given: \"$.paths['/api/{pluralApiId}/{documentId}'][*].parameters[*]\"\n    then:\n      field: \"name\"\n      function: enumeration\n      functionOptions:\n        values:\n          - documentId\n          - pluralApiId\n\n  strapi-pagination-parameters:\n    description: >-\n      Strapi list endpoints support both page-based (pagination[page] /\n      pagination[pageSize]) and offset-based (pagination[start]\
  \ /\n      pagination[limit]) pagination. Both styles use bracket notation.\n    message: \"List endpoints should document pagination parameters using bracket notation\"\n    severity: info\n    given: \"$.paths[*][get].parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^page$|^pageSize$|^limit$|^offset$\"\n\n  strapi-error-schema-shape:\n    description: >-\n      Strapi error responses follow a consistent shape with a top-level\n      'data' (null) property and an 'error' object containing 'status',\n      'name', 'message', and 'details'.\n    message: \"Error schema must include 'data' and 'error' properties\"\n    severity: warn\n    given: \"$.components.schemas.Error.properties\"\n    then:\n      - function: truthy\n        field: \"data\"\n      - function: truthy\n        field: \"error\"\n\n  strapi-operation-summaries-present:\n    description: >-\n      All operations must have a summary. Strapi docs use action-noun\n    \
  \  format (e.g., 'List content entries', 'Create a content entry').\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: truthy\n      field: \"summary\"\n\n  strapi-upload-multipart:\n    description: >-\n      Strapi file upload endpoints must use multipart/form-data content type.\n    message: \"Upload endpoint must use multipart/form-data\"\n    severity: warn\n    given: \"$.paths['/api/upload'][post].requestBody.content\"\n    then:\n      function: truthy\n      field: \"multipart/form-data\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/strapi/refs/heads/main/rules/strapi-rules.yml
tags:
- CMS
- Content Management
- Headless CMS
- Node.js
- Open Source
- Spectral
- Linting
- API Governance
---
