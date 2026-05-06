---
api_specs:
- filename: rackspace-cloud-dns.yaml
  format: yaml
  label: Rackspace Cloud DNS API
  slug: cloud-dns-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/openapi/rackspace-cloud-dns.yaml
- filename: rackspace-customer-service.yaml
  format: yaml
  label: Rackspace Customer Service API
  slug: customer-service-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/openapi/rackspace-customer-service.yaml
- filename: rackspace-cloud-identity.yaml
  format: yaml
  label: Rackspace Customer Identity API
  slug: customer-identity-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/openapi/rackspace-cloud-identity.yaml
- filename: rackspace-offer.yaml
  format: yaml
  label: Rackspace Offer API
  slug: offer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/openapi/rackspace-offer.yaml
categories:
- rackspace
description: Spectral linting rules defining API design standards and conventions for Rackspace Technology.
layout: rules
name: Rackspace Technology API Rules
provider_name: Rackspace Technology
provider_slug: rackspace-technology
rule_count: 34
rules:
- description: API title should begin with "Rackspace ".
  given: $.info
  name: rackspace-info-title
  severity: error
- description: API description must be present and substantive (>= 80 chars).
  given: $.info
  name: rackspace-info-description-required
  severity: error
- description: API version is required.
  given: $.info
  name: rackspace-info-version-required
  severity: error
- description: Contact information should be provided.
  given: $.info
  name: rackspace-info-contact-required
  severity: warn
- description: License should be provided (Apache 2.0 is standard for Rackspace OSS).
  given: $.info
  name: rackspace-info-license-required
  severity: warn
- description: Use OpenAPI 3.0.x.
  given: $
  name: rackspace-openapi-version
  severity: error
- description: At least one server must be defined.
  given: $
  name: rackspace-servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: rackspace-servers-https
  severity: error
- description: Production servers should be hosted under the rackspacecloud.com or rackspace.com domains.
  given: $.servers[*]
  name: rackspace-servers-rackspacecloud
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths
  name: rackspace-paths-no-trailing-slash
  severity: error
- description: Path segments should be lowercase, kebab-case, or camelCase identifiers (no UPPER_SNAKE_CASE except curly-brace path params).
  given: $.paths
  name: rackspace-paths-kebab-or-lowercase
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-id-required
  severity: error
- description: operationId must use camelCase (verb prefix preferred — get/list/show/create/update/delete/add).
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-id-camelcase
  severity: error
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-summary-required
  severity: error
- description: Operation summaries should use Title Case (each major word capitalized).
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-description-required
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: rackspace-operation-tags-required
  severity: error
- description: Tags must be declared at the root level.
  given: $
  name: rackspace-tags-defined
  severity: warn
- description: Tag names should be PascalCase or Title Case (e.g. CustomerAccounts, Reverse DNS).
  given: $.tags[*]
  name: rackspace-tags-pascal-case
  severity: warn
- description: All parameters must have a description.
  given: $..parameters[?(@.in)]
  name: rackspace-parameter-description-required
  severity: warn
- description: All parameters must have a schema.
  given: $..parameters[?(@.in)]
  name: rackspace-parameter-schema-required
  severity: error
- description: Parameter names should be camelCase (Rackspace convention).
  given: $..parameters[?(@.in == 'query' || @.in == 'header')]
  name: rackspace-parameter-camelcase
  severity: warn
- description: Pagination should use limit + offset (Cloud DNS, Identity) or limit + marker (Offer API).
  given: $.paths[*][get].parameters[?(@.in == 'query')]
  name: rackspace-pagination-limit-offset
  severity: hint
- description: Every response object must have a description.
  given: $.paths[*][*].responses[*]
  name: rackspace-response-description-required
  severity: error
- description: Every operation must declare a 2xx success response.
  given: $.paths[*][get,post,put,patch,delete]
  name: rackspace-response-success-required
  severity: error
- description: Tenant-scoped operations should declare a 401 Unauthorized response.
  given: $.paths[?(@property.match(/\\{account\\}|\\{tenantId\\}/))][get,post,put,patch,delete].responses
  name: rackspace-response-error-401
  severity: warn
- description: Mutating Cloud DNS operations should return 202 Accepted (async job pattern).
  given: $.paths[?(@property.match(/dns|domains/))][post,put,delete].responses
  name: rackspace-response-async-job-202
  severity: warn
- description: JSON properties should be camelCase (Rackspace Java/Jackson convention).
  given: $.components.schemas[*].properties
  name: rackspace-schema-property-camelcase
  severity: warn
- description: Schema properties must declare a type or $ref.
  given: $.components.schemas[*].properties[*]
  name: rackspace-schema-types-defined
  severity: warn
- description: Global security must be defined.
  given: $
  name: rackspace-security-global
  severity: error
- description: Rackspace APIs use the X-Auth-Token header (Cloud Identity-issued bearer token).
  given: $.components.securitySchemes[*]
  name: rackspace-security-x-auth-token
  severity: warn
- description: GET operations must not have a requestBody.
  given: $.paths[*].get
  name: rackspace-get-no-request-body
  severity: error
- description: DELETE operations should not have a requestBody (use query parameters).
  given: $.paths[*].delete
  name: rackspace-delete-no-request-body
  severity: warn
- description: Operations should include x-microcks-operation for mock dispatching.
  given: $.paths[*][get,post,put,patch,delete]
  name: rackspace-microcks-extension
  severity: hint
rules_file: rules/rackspace-technology-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/rules/rackspace-technology-rules.yml
severity_counts:
  error: 16
  hint: 2
  info: 0
  warn: 16
slug: rackspace-technology-rules
source_filename: rackspace-technology-rules.yml
source_heading: Spectral Ruleset
source_yaml: "# Rackspace Technology — Spectral Ruleset\n#\n# Opinionated rules derived from the four Rackspace OpenAPI specs in this\n# repo (Cloud DNS, Cloud Identity, Customer Service, Offer). The rules\n# enforce conventions Rackspace docs and SDK code consistently use:\n# - X-Auth-Token-based authentication (Cloud Identity-issued tokens)\n# - kebab-case (or lowercase) path segments under tenant-scoped /{account}\n# - camelCase JSON property names (Java/Jackson convention)\n# - 202 Accepted for async DNS jobs, 200 for synchronous reads\n# - Title Case tag names\n\nextends: [\"spectral:oas\"]\n\nfunctions: []\n\nrules:\n  # ---------------------------------------------------------------------\n  # INFO / METADATA\n  # ---------------------------------------------------------------------\n  rackspace-info-title:\n    description: API title should begin with \"Rackspace \".\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: pattern\n      functionOptions:\n\
  \        match: \"^Rackspace \"\n  rackspace-info-description-required:\n    description: API description must be present and substantive (>= 80 chars).\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: length\n      functionOptions:\n        min: 80\n  rackspace-info-version-required:\n    description: API version is required.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n  rackspace-info-contact-required:\n    description: Contact information should be provided.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n  rackspace-info-license-required:\n    description: License should be provided (Apache 2.0 is standard for Rackspace OSS).\n    severity: warn\n    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  # ---------------------------------------------------------------------\n  # OPENAPI VERSION\n  # ---------------------------------------------------------------------\n\
  \  rackspace-openapi-version:\n    description: Use OpenAPI 3.0.x.\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # ---------------------------------------------------------------------\n  # SERVERS\n  # ---------------------------------------------------------------------\n  rackspace-servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n  rackspace-servers-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n  rackspace-servers-rackspacecloud:\n    description: Production servers should be hosted under the rackspacecloud.com or rackspace.com domains.\n    severity: warn\n    given: $.servers[*]\n    then:\n    \
  \  field: url\n      function: pattern\n      functionOptions:\n        match: \"(rackspacecloud\\\\.com|rackspace\\\\.com)\"\n\n  # ---------------------------------------------------------------------\n  # PATHS — NAMING CONVENTIONS\n  # ---------------------------------------------------------------------\n  rackspace-paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n      field: \"@key\"\n  rackspace-paths-kebab-or-lowercase:\n    description: Path segments should be lowercase, kebab-case, or camelCase identifiers (no UPPER_SNAKE_CASE except curly-brace path params).\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-zA-Z0-9_\\\\-:.]*|/\\\\{[a-zA-Z0-9_]+\\\\}|/v[0-9]+(\\\\.[0-9]+)?)+$\"\n      field: \"@key\"\n\n  # ---------------------------------------------------------------------\n\
  \  # OPERATIONS\n  # ---------------------------------------------------------------------\n  rackspace-operation-id-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: operationId\n      function: truthy\n  rackspace-operation-id-camelcase:\n    description: operationId must use camelCase (verb prefix preferred — get/list/show/create/update/delete/add).\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n  rackspace-operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: summary\n      function: truthy\n  rackspace-operation-summary-title-case:\n    description: Operation\
  \ summaries should use Title Case (each major word capitalized).\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: summary\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*([ \\\\-/][A-Z0-9][A-Za-z0-9]*)*$\"\n  rackspace-operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: description\n      function: truthy\n  rackspace-operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # ---------------------------------------------------------------------\n  # TAGS\n  # ---------------------------------------------------------------------\n\
  \  rackspace-tags-defined:\n    description: Tags must be declared at the root level.\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n  rackspace-tags-pascal-case:\n    description: Tag names should be PascalCase or Title Case (e.g. CustomerAccounts, Reverse DNS).\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*( [A-Z][A-Za-z0-9]*)*$\"\n\n  # ---------------------------------------------------------------------\n  # PARAMETERS\n  # ---------------------------------------------------------------------\n  rackspace-parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: $..parameters[?(@.in)]\n    then:\n      field: description\n      function: truthy\n  rackspace-parameter-schema-required:\n    description: All parameters must have a schema.\n    severity: error\n    given:\
  \ $..parameters[?(@.in)]\n    then:\n      field: schema\n      function: truthy\n  rackspace-parameter-camelcase:\n    description: Parameter names should be camelCase (Rackspace convention).\n    severity: warn\n    given: $..parameters[?(@.in == 'query' || @.in == 'header')]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^[a-zA-Z][a-zA-Z0-9_\\\\-]*$\"\n  rackspace-pagination-limit-offset:\n    description: Pagination should use limit + offset (Cloud DNS, Identity) or limit + marker (Offer API).\n    severity: hint\n    given: $.paths[*][get].parameters[?(@.in == 'query')]\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values: [limit, offset, marker, name, type, data, status, lineOfBusiness, apply_rcn_roles, include_endpoints, include_accessible_domains, belongsTo, showRecords, showSubdomains, deleteSubdomains, changes, cloneName, cloneSubdomains, modifyRecordData, modifyEmailAddress, modifyComment,\
  \ href, ip, id, key, offeringCode, offeringVersion]\n\n  # ---------------------------------------------------------------------\n  # RESPONSES\n  # ---------------------------------------------------------------------\n  rackspace-response-description-required:\n    description: Every response object must have a description.\n    severity: error\n    given: $.paths[*][*].responses[*]\n    then:\n      field: description\n      function: truthy\n  rackspace-response-success-required:\n    description: Every operation must declare a 2xx success response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2[0-9][0-9]$\": {}\n          minProperties: 1\n  rackspace-response-error-401:\n    description: Tenant-scoped operations should declare a 401 Unauthorized response.\n    severity: warn\n    given:\
  \ $.paths[?(@property.match(/\\\\{account\\\\}|\\\\{tenantId\\\\}/))][get,post,put,patch,delete].responses\n    then:\n      field: \"401\"\n      function: truthy\n  rackspace-response-async-job-202:\n    description: Mutating Cloud DNS operations should return 202 Accepted (async job pattern).\n    severity: warn\n    given: $.paths[?(@property.match(/dns|domains/))][post,put,delete].responses\n    then:\n      field: \"202\"\n      function: truthy\n\n  # ---------------------------------------------------------------------\n  # SCHEMAS — PROPERTY NAMING\n  # ---------------------------------------------------------------------\n  rackspace-schema-property-camelcase:\n    description: JSON properties should be camelCase (Rackspace Java/Jackson convention).\n    severity: warn\n    given: $.components.schemas[*].properties\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9_\\\\-]*$|^RAX-AUTH:[a-zA-Z]+$|^OS-KSADM:[a-zA-Z]+$|^RAX-KSKEY:[a-zA-Z]+$\"\
  \n      field: \"@key\"\n  rackspace-schema-types-defined:\n    description: Schema properties must declare a type or $ref.\n    severity: warn\n    given: $.components.schemas[*].properties[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [type]\n            - required: [$ref]\n            - required: [allOf]\n            - required: [oneOf]\n            - required: [anyOf]\n            - required: [enum]\n            - required: [additionalProperties]\n\n  # ---------------------------------------------------------------------\n  # SECURITY\n  # ---------------------------------------------------------------------\n  rackspace-security-global:\n    description: Global security must be defined.\n    severity: error\n    given: $\n    then:\n      field: security\n      function: truthy\n  rackspace-security-x-auth-token:\n    description: Rackspace APIs use the X-Auth-Token header (Cloud Identity-issued bearer token).\n\
  \    severity: warn\n    given: $.components.securitySchemes[*]\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type: { const: apiKey }\n            in: { const: header }\n            name: { const: X-Auth-Token }\n          required: [type, in, name]\n\n  # ---------------------------------------------------------------------\n  # HTTP METHOD CONVENTIONS\n  # ---------------------------------------------------------------------\n  rackspace-get-no-request-body:\n    description: GET operations must not have a requestBody.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n  rackspace-delete-no-request-body:\n    description: DELETE operations should not have a requestBody (use query parameters).\n    severity: warn\n    given: $.paths[*].delete\n    then:\n      field: requestBody\n      function: falsy\n\n  # ---------------------------------------------------------------------\n\
  \  # GENERAL QUALITY\n  # ---------------------------------------------------------------------\n  rackspace-microcks-extension:\n    description: Operations should include x-microcks-operation for mock dispatching.\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rackspace-technology/refs/heads/main/rules/rackspace-technology-rules.yml
tags:
- Cloud
- Managed Services
- Multicloud
- Infrastructure
- DevOps
- Spectral
- Linting
- API Governance
---
