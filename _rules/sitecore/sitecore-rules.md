---
api_specs:
- filename: sitecore-xm-cloud-rest-api-openapi.yml
  format: yaml
  label: Sitecore XM Cloud REST API
  slug: xm-cloud-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-xm-cloud-rest-api-openapi.yml
- filename: sitecore-cdp-rest-api-openapi.yml
  format: yaml
  label: Sitecore CDP REST API
  slug: cdp-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-cdp-rest-api-openapi.yml
- filename: sitecore-cdp-stream-api-asyncapi.yml
  format: yaml
  label: Sitecore CDP Stream API
  slug: cdp-stream-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/asyncapi/sitecore-cdp-stream-api-asyncapi.yml
- filename: sitecore-personalize-rest-api-openapi.yml
  format: yaml
  label: Sitecore Personalize REST API
  slug: personalize-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-personalize-rest-api-openapi.yml
- filename: sitecore-content-hub-rest-api-openapi.yml
  format: yaml
  label: Sitecore Content Hub REST API
  slug: content-hub-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-content-hub-rest-api-openapi.yml
- filename: sitecore-ordercloud-api-openapi.yml
  format: yaml
  label: Sitecore OrderCloud API
  slug: ordercloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-ordercloud-api-openapi.yml
- filename: sitecore-discover-api-openapi.yml
  format: yaml
  label: Sitecore Discover API
  slug: discover-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/openapi/sitecore-discover-api-openapi.yml
categories:
- sitecore
description: Spectral linting rules defining API design standards and conventions for sitecore.
layout: rules
name: sitecore API Rules
provider_name: sitecore
provider_slug: sitecore
rule_count: 14
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sitecore-operation-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: sitecore-operation-id-camel-case
  severity: error
- description: Path segments must use kebab-case or camelCase (no underscores)
  given: $.paths
  name: sitecore-path-kebab-case
  severity: warn
- description: Security schemes must be Bearer token or Basic Auth (Sitecore standard)
  given: $.components.securitySchemes[*]
  name: sitecore-bearer-or-basic-auth
  severity: error
- description: All 200 responses must define a schema
  given: $.paths[*][*].responses['200'].content['application/json']
  name: sitecore-response-200-has-schema
  severity: warn
- description: 400 error responses should reference a ProblemDetails or error schema
  given: $.paths[*][*].responses['400']
  name: sitecore-400-uses-problem-details
  severity: info
- description: Operation tags must correspond to tags defined in the root tags array
  given: $.paths[*][*].tags[*]
  name: sitecore-tags-must-match-defined
  severity: warn
- description: API paths should include a version prefix (/v1/, /v2.1/, /authoring/)
  given: $.paths
  name: sitecore-versioned-path
  severity: info
- description: Paths must not end with a trailing slash
  given: $.paths
  name: sitecore-no-trailing-slash
  severity: error
- description: POST operations that create or update resources must have a request body
  given: $.paths[*].post
  name: sitecore-post-has-request-body
  severity: warn
- description: DELETE operations should return 204 No Content on success
  given: $.paths[*].delete.responses
  name: sitecore-delete-returns-204
  severity: info
- description: List operations should support pagination parameters
  given: $.paths[*].get
  name: sitecore-list-operations-paginated
  severity: info
- description: The info section must include a contact object
  given: $.info
  name: sitecore-info-contact-defined
  severity: warn
- description: At least one server must be defined
  given: $
  name: sitecore-servers-defined
  severity: error
rules_file: rules/sitecore-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/rules/sitecore-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 4
  warn: 6
slug: sitecore-rules
source_filename: sitecore-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sitecore-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*(\\\\s[A-Za-z][a-z]*)*)(\\\\s[A-Za-z][a-z]*)*$\"\n\n  sitecore-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sitecore-path-kebab-case:\n    description: Path segments must use kebab-case or camelCase (no underscores)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-zA-Z0-9{}\\\\-\\\\.]+)*$\"\n\n  sitecore-bearer-or-basic-auth:\n    description: Security schemes must be Bearer token or Basic Auth (Sitecore standard)\n   \
  \ severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  enum: [bearer, basic]\n            - properties:\n                type:\n                  const: apiKey\n\n  sitecore-response-200-has-schema:\n    description: All 200 responses must define a schema\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  sitecore-400-uses-problem-details:\n    description: 400 error responses should reference a ProblemDetails or error schema\n    severity: info\n    given: \"$.paths[*][*].responses['400']\"\n    then:\n      function: truthy\n\n  sitecore-tags-must-match-defined:\n    description: Operation tags must correspond to tags defined in the root tags array\n    severity:\
  \ warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z\\\\s]*$\"\n\n  sitecore-versioned-path:\n    description: API paths should include a version prefix (/v1/, /v2.1/, /authoring/)\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/(?:v[0-9]+(\\\\.[0-9]+)?|api\\\\/v[0-9]+|authoring)\\\\/.*$\"\n\n  sitecore-no-trailing-slash:\n    description: Paths must not end with a trailing slash\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  sitecore-post-has-request-body:\n    description: POST operations that create or update resources must have a request body\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  sitecore-delete-returns-204:\n    description: DELETE operations should\
  \ return 204 No Content on success\n    severity: info\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  sitecore-list-operations-paginated:\n    description: List operations should support pagination parameters\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  sitecore-info-contact-defined:\n    description: The info section must include a contact object\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sitecore-servers-defined:\n    description: At least one server must be defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sitecore/refs/heads/main/rules/sitecore-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
