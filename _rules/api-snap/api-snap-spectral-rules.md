---
api_specs:
- filename: api-snap-openapi.yml
  format: yaml
  label: QR Code API
  slug: qr
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Screenshot API
  slug: screenshot
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Image Resize API
  slug: resize
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: PDF API
  slug: pdf
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Markdown API
  slug: markdown
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: URL Metadata API
  slug: meta
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Hash API
  slug: hash
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: JWT Decode API
  slug: jwt-decode
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Base64 API
  slug: base64
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: UUID API
  slug: uuid
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Color API
  slug: color
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Lorem Ipsum API
  slug: lorem
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
- filename: api-snap-openapi.yml
  format: yaml
  label: Placeholder Image API
  slug: placeholder
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/openapi/api-snap-openapi.yml
categories:
- examples
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- post
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for API Snap.
layout: rules
name: API Snap API Rules
provider_name: API Snap
provider_slug: api-snap
rule_count: 37
rules:
- description: Spec must declare an info.title.
  given: $.info
  name: info-title-required
  severity: error
- description: Spec must declare an info.description with at least 60 characters.
  given: $.info
  name: info-description-required
  severity: warn
- description: Spec must declare info.version.
  given: $.info
  name: info-version-required
  severity: error
- description: Spec must declare info.contact with name and url.
  given: $.info.contact
  name: info-contact-required
  severity: warn
- description: API Snap uses OpenAPI 3.0.3.
  given: $.openapi
  name: openapi-version-3-0-3
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All servers must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Production server should be https://api-snap.com.
  given: $.servers[*].url
  name: servers-api-snap
  severity: info
- description: All paths must be prefixed with /api/.
  given: $.paths
  name: paths-api-prefix
  severity: error
- description: Path segments must be lowercase kebab-case (e.g. /api/jwt-decode).
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary in Title Case.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId must be camelCase (e.g. generateQrCode, captureScreenshot).
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: operationId should start with a recognized verb (generate, capture, convert, hash, resize, decode, extract, base64).
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-verb-prefix
  severity: info
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Tags must use PascalCase (e.g. Images, Browser, Documents, Security, Utilities).
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: tags-pascal-case
  severity: warn
- description: Tags should be one of the documented categories.
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: tags-from-allowed-set
  severity: info
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Query parameters use snake_case (full_page) when multi-word.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in=='query')].name
  name: parameter-snake-case
  severity: info
- description: api_key query parameter is permitted as an Authorization header alias.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name=='api_key')]
  name: parameter-api-key-allowed
  severity: info
- description: Request bodies must declare a content map.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-content-required
  severity: error
- description: Request bodies should use application/json or multipart/form-data.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-json-or-multipart
  severity: warn
- description: Every operation must declare a 200 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-200-required
  severity: error
- description: Every operation must declare a 401 response (missing/invalid API key).
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: Every operation must declare a 429 response (rate limit exceeded).
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-429-required
  severity: warn
- description: Each response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: warn
- description: JSON body and response properties use camelCase (urlSafe, expiresAt).
  given: $.components.schemas[*].properties
  name: schema-camel-case-properties
  severity: info
- description: Schema properties must declare a type or $ref.
  given: $.components.schemas[*].properties[*]
  name: schema-type-required
  severity: warn
- description: components.securitySchemes must define at least one scheme.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: BearerAuth security scheme must be defined for the snp_ API key.
  given: $.components.securitySchemes
  name: security-bearer-auth
  severity: warn
- description: Top-level security must be declared and reference BearerAuth.
  given: $
  name: security-global-required
  severity: warn
- description: GET operations must not declare a requestBody.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should declare a requestBody.
  given: $.paths[*].post
  name: post-has-request-body
  severity: warn
- description: Operations should include at least one example for response or request.
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: examples-encouraged
  severity: info
- description: Operations should include x-microcks-operation for mock-server compatibility.
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-extension-encouraged
  severity: info
rules_file: rules/api-snap-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/rules/api-snap-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 8
  warn: 18
slug: api-snap-spectral-rules
source_filename: api-snap-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - [spectral:oas, recommended]\n\n# Spectral ruleset for API Snap (https://api-snap.com/)\n# Enforces the conventions observed across the api-snap-openapi.yml spec:\n#   - OpenAPI 3.0.3\n#   - Single base server: https://api-snap.com\n#   - All paths under /api with kebab-case (jwt-decode)\n#   - camelCase operationIds with verb prefixes (generate*, capture*, decode*, convert*, extract*, hash*, resize*)\n#   - PascalCase tags (Images, Browser, Documents, Security, Utilities)\n#   - snake_case query parameters (full_page) and camelCase JSON body properties (urlSafe, expiresAt)\n#   - Bearer auth via Authorization header (snp_ prefix) with api_key query alias\n#   - Standard error response set: 400, 401, 429\nrules:\n\n  # ----------------------------------------------------------------\n  # INFO / METADATA\n  # ----------------------------------------------------------------\n  info-title-required:\n    description: Spec must declare an info.title.\n    given: $.info\n\
  \    severity: error\n    then:\n      field: title\n      function: truthy\n  info-description-required:\n    description: Spec must declare an info.description with at least 60 characters.\n    given: $.info\n    severity: warn\n    then:\n      field: description\n      function: length\n      functionOptions:\n        min: 60\n  info-version-required:\n    description: Spec must declare info.version.\n    given: $.info\n    severity: error\n    then:\n      field: version\n      function: truthy\n  info-contact-required:\n    description: Spec must declare info.contact with name and url.\n    given: $.info.contact\n    severity: warn\n    then:\n      - field: name\n        function: truthy\n      - field: url\n        function: truthy\n\n  # ----------------------------------------------------------------\n  # OPENAPI VERSION\n  # ----------------------------------------------------------------\n  openapi-version-3-0-3:\n    description: API Snap uses OpenAPI 3.0.3.\n    given: $.openapi\n\
  \    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: ^3\\.0\\.\\d+$\n\n  # ----------------------------------------------------------------\n  # SERVERS\n  # ----------------------------------------------------------------\n  servers-defined:\n    description: At least one server must be defined.\n    given: $\n    severity: error\n    then:\n      field: servers\n      function: truthy\n  servers-https:\n    description: All servers must use HTTPS.\n    given: $.servers[*].url\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: ^https://\n  servers-api-snap:\n    description: Production server should be https://api-snap.com.\n    given: $.servers[*].url\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: ^https://api-snap\\.com\n\n  # ----------------------------------------------------------------\n  # PATHS - NAMING CONVENTIONS\n  # ----------------------------------------------------------------\n\
  \  paths-api-prefix:\n    description: All paths must be prefixed with /api/.\n    given: $.paths\n    severity: error\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: ^/api/\n  paths-kebab-case:\n    description: Path segments must be lowercase kebab-case (e.g. /api/jwt-decode).\n    given: $.paths\n    severity: warn\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: ^/[a-z0-9/-]+$\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    given: $.paths\n    severity: warn\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        notMatch: .+/$\n\n  # ----------------------------------------------------------------\n  # OPERATIONS\n  # ----------------------------------------------------------------\n  operation-summary-required:\n    description: Every operation must have a summary in Title Case.\n    given: $.paths[*][get,post,put,patch,delete]\n\
  \    severity: error\n    then:\n      field: summary\n      function: truthy\n  operation-description-required:\n    description: Every operation should have a description.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: warn\n    then:\n      field: description\n      function: truthy\n  operation-id-required:\n    description: Every operation must have an operationId.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n  operation-id-camel-case:\n    description: operationId must be camelCase (e.g. generateQrCode, captureScreenshot).\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: ^[a-z][a-zA-Z0-9]+$\n  operation-id-verb-prefix:\n    description: operationId should start with a recognized verb (generate, capture, convert, hash, resize, decode, extract, base64).\n    given: $.paths[*][get,post,put,patch,delete].operationId\n\
  \    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: ^(generate|capture|convert|hash|resize|decode|extract|base64|html|markdown)\n  operation-tags-required:\n    description: Every operation must declare at least one tag.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: warn\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  # ----------------------------------------------------------------\n  # TAGS\n  # ----------------------------------------------------------------\n  tags-pascal-case:\n    description: Tags must use PascalCase (e.g. Images, Browser, Documents, Security, Utilities).\n    given: $.paths[*][get,post,put,patch,delete].tags[*]\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: ^[A-Z][a-zA-Z]+$\n  tags-from-allowed-set:\n    description: Tags should be one of the documented categories.\n    given: $.paths[*][get,post,put,patch,delete].tags[*]\n\
  \    severity: info\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Images\n          - Browser\n          - Documents\n          - Security\n          - Utilities\n\n  # ----------------------------------------------------------------\n  # PARAMETERS\n  # ----------------------------------------------------------------\n  parameter-description-required:\n    description: Every parameter must have a description.\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    severity: warn\n    then:\n      field: description\n      function: truthy\n  parameter-snake-case:\n    description: Query parameters use snake_case (full_page) when multi-word.\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in=='query')].name\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: ^[a-z][a-z0-9_]*$\n  parameter-api-key-allowed:\n    description: api_key query parameter is permitted as an\
  \ Authorization header alias.\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name=='api_key')]\n    severity: info\n    then:\n      function: truthy\n\n  # ----------------------------------------------------------------\n  # REQUEST BODIES\n  # ----------------------------------------------------------------\n  request-body-content-required:\n    description: Request bodies must declare a content map.\n    given: $.paths[*][post,put,patch].requestBody\n    severity: error\n    then:\n      field: content\n      function: truthy\n  request-body-json-or-multipart:\n    description: Request bodies should use application/json or multipart/form-data.\n    given: $.paths[*][post,put,patch].requestBody.content\n    severity: warn\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: ^(application/json|multipart/form-data)$\n\n  # ----------------------------------------------------------------\n  # RESPONSES\n  # ----------------------------------------------------------------\n\
  \  response-200-required:\n    description: Every operation must declare a 200 success response.\n    given: $.paths[*][get,post,put,patch,delete].responses\n    severity: error\n    then:\n      field: '200'\n      function: truthy\n  response-401-required:\n    description: Every operation must declare a 401 response (missing/invalid API key).\n    given: $.paths[*][get,post,put,patch,delete].responses\n    severity: warn\n    then:\n      field: '401'\n      function: truthy\n  response-429-required:\n    description: Every operation must declare a 429 response (rate limit exceeded).\n    given: $.paths[*][get,post,put,patch,delete].responses\n    severity: warn\n    then:\n      field: '429'\n      function: truthy\n  response-description-required:\n    description: Each response must have a description.\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  # ----------------------------------------------------------------\n\
  \  # SCHEMAS - PROPERTY NAMING\n  # ----------------------------------------------------------------\n  schema-camel-case-properties:\n    description: JSON body and response properties use camelCase (urlSafe, expiresAt).\n    given: $.components.schemas[*].properties\n    severity: info\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: ^[a-z][a-zA-Z0-9]*$\n  schema-type-required:\n    description: Schema properties must declare a type or $ref.\n    given: $.components.schemas[*].properties[*]\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [type]\n            - required: [$ref]\n            - required: [oneOf]\n            - required: [anyOf]\n            - required: [allOf]\n\n  # ----------------------------------------------------------------\n  # SECURITY\n  # ----------------------------------------------------------------\n  security-schemes-defined:\n\
  \    description: components.securitySchemes must define at least one scheme.\n    given: $.components\n    severity: error\n    then:\n      field: securitySchemes\n      function: truthy\n  security-bearer-auth:\n    description: BearerAuth security scheme must be defined for the snp_ API key.\n    given: $.components.securitySchemes\n    severity: warn\n    then:\n      field: BearerAuth\n      function: truthy\n  security-global-required:\n    description: Top-level security must be declared and reference BearerAuth.\n    given: $\n    severity: warn\n    then:\n      field: security\n      function: truthy\n\n  # ----------------------------------------------------------------\n  # HTTP METHOD CONVENTIONS\n  # ----------------------------------------------------------------\n  get-no-request-body:\n    description: GET operations must not declare a requestBody.\n    given: $.paths[*].get\n    severity: error\n    then:\n      field: requestBody\n      function: falsy\n  post-has-request-body:\n\
  \    description: POST operations should declare a requestBody.\n    given: $.paths[*].post\n    severity: warn\n    then:\n      field: requestBody\n      function: truthy\n\n  # ----------------------------------------------------------------\n  # GENERAL QUALITY\n  # ----------------------------------------------------------------\n  examples-encouraged:\n    description: Operations should include at least one example for response or request.\n    given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]\n    severity: info\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [example]\n            - required: [examples]\n  microcks-extension-encouraged:\n    description: Operations should include x-microcks-operation for mock-server compatibility.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: info\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/api-snap/refs/heads/main/rules/api-snap-spectral-rules.yml
tags:
- API Utilities
- Developer Tools
- QR Codes
- Screenshots
- Image Processing
- PDF Generation
- Markdown
- URL Metadata
- Hashing
- JWT
- Base64
- UUID
- Color Conversion
- Lorem Ipsum
- Placeholder Images
- Spectral
- Linting
- API Governance
---
