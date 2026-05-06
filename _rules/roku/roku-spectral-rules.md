---
api_specs:
- filename: roku-external-control-protocol.yaml
  format: yaml
  label: Roku External Control Protocol (ECP)
  slug: external-control-protocol
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/roku/refs/heads/main/openapi/roku-external-control-protocol.yaml
- filename: roku-pay-web-services.yaml
  format: yaml
  label: Roku Pay Web Services
  slug: pay
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/roku/refs/heads/main/openapi/roku-pay-web-services.yaml
- filename: roku-nabu-cloud.yaml
  format: yaml
  label: Roku Nabu Cloud
  slug: nabu-cloud
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/roku/refs/heads/main/openapi/roku-nabu-cloud.yaml
categories:
- roku
description: Spectral linting rules defining API design standards and conventions for Roku.
layout: rules
name: Roku API Rules
provider_name: Roku
provider_slug: roku
rule_count: 27
rules:
- description: API title should begin with "Roku".
  given: $.info.title
  name: roku-info-title-prefix
  severity: warn
- description: API info.description is required and should be at least 80 characters.
  given: $.info
  name: roku-info-description-required
  severity: error
- description: API info.version is required.
  given: $.info
  name: roku-info-version-required
  severity: error
- description: info.contact should be defined with a name or url.
  given: $.info
  name: roku-info-contact-required
  severity: warn
- description: Use OpenAPI 3.0.3 or 3.1.x.
  given: $.openapi
  name: roku-openapi-version
  severity: warn
- description: At least one server must be defined.
  given: $
  name: roku-servers-defined
  severity: error
- description: Production servers should use https. ECP local-network endpoints are an explicit exception (port 8060 plain HTTP).
  given: $.servers[*].url
  name: roku-servers-https-preferred
  severity: info
- description: Paths should not end with a trailing slash.
  given: $.paths
  name: roku-path-no-trailing-slash
  severity: warn
- description: Paths must not contain query strings.
  given: $.paths
  name: roku-path-no-query-string
  severity: error
- description: Path segments should be kebab-case or snake_case (no PascalCase or spaces).
  given: $.paths
  name: roku-path-allowed-casing
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: roku-operation-operationid-required
  severity: error
- description: Every operation must have a summary.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: roku-operation-summary-required
  severity: error
- description: Operation summaries should begin with "Roku ".
  given: $.paths.*[get,post,put,patch,delete,head,options].summary
  name: roku-operation-summary-prefix
  severity: warn
- description: Every operation should have a description.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: roku-operation-description-required
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: roku-operation-tags-required
  severity: warn
- description: Operations should declare an x-microcks-operation extension for mock dispatch.
  given: $.paths.*[get,post,put,patch,delete,head,options]
  name: roku-operation-microcks-extension
  severity: info
- description: A global tags array should be defined at the document root.
  given: $
  name: roku-tags-defined
  severity: warn
- description: Each tag should have a description.
  given: $.tags[*]
  name: roku-tag-description
  severity: info
- description: Each parameter must have a description.
  given: $..parameters[?(@.in)]
  name: roku-parameter-description
  severity: warn
- description: Each parameter must declare a schema with a type.
  given: $..parameters[?(@.in)]
  name: roku-parameter-schema
  severity: error
- description: Request bodies should support application/json.
  given: $..requestBody.content
  name: roku-requestbody-json
  severity: warn
- description: Every operation must declare a 2xx success response.
  given: $.paths.*[get,post,put,patch,delete,head,options].responses
  name: roku-response-success-required
  severity: error
- description: Every response must have a description.
  given: $..responses.*
  name: roku-response-description
  severity: warn
- description: Top-level component schemas should declare a type.
  given: $.components.schemas.*
  name: roku-schema-type-required
  severity: warn
- description: Schemas extracted from documentation, SDK, or samples should declare x-schema-source for traceability.
  given: $.components.schemas.*
  name: roku-schema-source-extension
  severity: info
- description: Security schemes should declare a description.
  given: $.components.securitySchemes.*
  name: roku-security-schemes-described
  severity: info
- description: Specs generated from documentation should declare x-source-url for traceability.
  given: $.info
  name: roku-info-x-source-url
  severity: info
rules_file: rules/roku-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/roku/refs/heads/main/rules/roku-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 6
  warn: 13
slug: roku-spectral-rules
source_filename: roku-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\n# Roku API Spectral Ruleset\n# Enforces conventions observed across the Roku Nabu Cloud, External Control Protocol (ECP),\n# and Roku Pay Web Services OpenAPI specifications.\n#\n# Casing dominance:\n#   - Operation IDs: camelCase / snake_case mixed (Nabu Cloud uses snake_case operationIds via tags;\n#     ECP and Roku Pay use camelCase). Enforce camelCase as the canonical convention going forward.\n#   - Path segments: kebab-case dominant (e.g., /validate-transaction, /query/active-app, /personal_access_tokens).\n#     The Nabu Cloud API uses snake_case for some path segments — relax this to allow either.\n#   - Schema property names: camelCase dominant in ECP and Roku Pay, snake_case in Nabu Cloud.\n#     Enforce that they are consistent within each spec.\n#   - Tag names: Title Case (e.g., \"Validation\", \"Apps\", \"KeyPress\" -> \"Key Press\").\n\nrules:\n\n  # ============================================================\n  # INFO / METADATA\n\
  \  # ============================================================\n\n  roku-info-title-prefix:\n    description: API title should begin with \"Roku\".\n    message: \"Title '{{value}}' should begin with 'Roku'.\"\n    severity: warn\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Roku\"\n\n  roku-info-description-required:\n    description: API info.description is required and should be at least 80 characters.\n    message: \"info.description must be present and substantive (>= 80 chars).\"\n    severity: error\n    given: $.info\n    then:\n      - field: description\n        function: truthy\n      - field: description\n        function: length\n        functionOptions:\n          min: 80\n\n  roku-info-version-required:\n    description: API info.version is required.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  roku-info-contact-required:\n    description: info.contact should\
  \ be defined with a name or url.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # ============================================================\n  # OPENAPI VERSION\n  # ============================================================\n\n  roku-openapi-version:\n    description: Use OpenAPI 3.0.3 or 3.1.x.\n    message: \"openapi version should be 3.0.x or 3.1.x.\"\n    severity: warn\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.[01]\\\\.\"\n\n  # ============================================================\n  # SERVERS\n  # ============================================================\n\n  roku-servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  roku-servers-https-preferred:\n    description: Production servers should use https. ECP local-network endpoints are an\
  \ explicit exception (port 8060 plain HTTP).\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(https://|http://\\\\{rokuDeviceIp\\\\}:8060)\"\n\n  # ============================================================\n  # PATHS - NAMING CONVENTIONS\n  # ============================================================\n\n  roku-path-no-trailing-slash:\n    description: Paths should not end with a trailing slash.\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      field: \"@key\"\n      functionOptions:\n        notMatch: \".+/$\"\n\n  roku-path-no-query-string:\n    description: Paths must not contain query strings.\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      field: \"@key\"\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  roku-path-allowed-casing:\n    description: Path segments should be kebab-case or snake_case (no PascalCase or spaces).\n\
  \    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      field: \"@key\"\n      functionOptions:\n        match: \"^(/(([a-z0-9][a-z0-9_-]*)|\\\\{[a-zA-Z_][a-zA-Z0-9_]*\\\\}))*/?$\"\n\n  # ============================================================\n  # OPERATIONS\n  # ============================================================\n\n  roku-operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  roku-operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  roku-operation-summary-prefix:\n    description: Operation summaries should begin with \"Roku \".\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options].summary\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"^Roku \"\n\n  roku-operation-description-required:\n    description: Every operation should have a description.\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  roku-operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  roku-operation-microcks-extension:\n    description: Operations should declare an x-microcks-operation extension for mock dispatch.\n    severity: info\n    given: $.paths.*[get,post,put,patch,delete,head,options]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  # ============================================================\n  # TAGS\n  # ============================================================\n\
  \n  roku-tags-defined:\n    description: A global tags array should be defined at the document root.\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  roku-tag-description:\n    description: Each tag should have a description.\n    severity: info\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n  # PARAMETERS\n  # ============================================================\n\n  roku-parameter-description:\n    description: Each parameter must have a description.\n    severity: warn\n    given: $..parameters[?(@.in)]\n    then:\n      field: description\n      function: truthy\n\n  roku-parameter-schema:\n    description: Each parameter must declare a schema with a type.\n    severity: error\n    given: $..parameters[?(@.in)]\n    then:\n      field: schema\n      function: truthy\n\n  # ============================================================\n\
  \  # REQUEST BODIES\n  # ============================================================\n\n  roku-requestbody-json:\n    description: Request bodies should support application/json.\n    severity: warn\n    given: $..requestBody.content\n    then:\n      field: application/json\n      function: truthy\n\n  # ============================================================\n  # RESPONSES\n  # ============================================================\n\n  roku-response-success-required:\n    description: Every operation must declare a 2xx success response.\n    severity: error\n    given: $.paths.*[get,post,put,patch,delete,head,options].responses\n    then:\n      function: pattern\n      field: \"@key\"\n      functionOptions:\n        match: \"^(2[0-9][0-9]|default)$\"\n\n  roku-response-description:\n    description: Every response must have a description.\n    severity: warn\n    given: $..responses.*\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n\
  \  # SCHEMAS\n  # ============================================================\n\n  roku-schema-type-required:\n    description: Top-level component schemas should declare a type.\n    severity: warn\n    given: $.components.schemas.*\n    then:\n      field: type\n      function: truthy\n\n  roku-schema-source-extension:\n    description: Schemas extracted from documentation, SDK, or samples should declare x-schema-source for traceability.\n    severity: info\n    given: $.components.schemas.*\n    then:\n      field: x-schema-source\n      function: truthy\n\n  # ============================================================\n  # SECURITY\n  # ============================================================\n\n  roku-security-schemes-described:\n    description: Security schemes should declare a description.\n    severity: info\n    given: $.components.securitySchemes.*\n    then:\n      field: description\n      function: truthy\n\n  # ============================================================\n\
  \  # GENERAL QUALITY\n  # ============================================================\n\n  roku-info-x-source-url:\n    description: Specs generated from documentation should declare x-source-url for traceability.\n    severity: info\n    given: $.info\n    then:\n      field: x-source-url\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/roku/refs/heads/main/rules/roku-spectral-rules.yml
tags:
- Streaming
- Television
- Media
- Entertainment
- Connected TV
- Consumer Electronics
- Spectral
- Linting
- API Governance
---
