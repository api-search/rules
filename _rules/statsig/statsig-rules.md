---
api_specs:
- filename: statsig-http-api-openapi.yml
  format: yaml
  label: Statsig HTTP API
  slug: http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-http-api-openapi.yml
- filename: statsig-console-api-openapi.yml
  format: yaml
  label: Statsig Console API
  slug: console-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-console-api-openapi.yml
- filename: statsig-client-sdk-api-openapi.yml
  format: yaml
  label: Statsig Client SDK API
  slug: client-sdk-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-client-sdk-api-openapi.yml
- filename: statsig-server-sdk-api-openapi.yml
  format: yaml
  label: Statsig Server SDK API
  slug: server-sdk-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-server-sdk-api-openapi.yml
- filename: statsig-events-api-openapi.yml
  format: yaml
  label: Statsig Events API
  slug: events-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/openapi/statsig-events-api-openapi.yml
categories:
- statsig
description: Spectral linting rules defining API design standards and conventions for statsig.
layout: rules
name: statsig API Rules
provider_name: statsig
provider_slug: statsig
rule_count: 10
rules:
- description: Statsig APIs require authentication via the statsig-api-key header. All operations must declare this security requirement.
  given: $.paths[*][*]
  name: statsig-api-key-header
  severity: error
- description: Statsig API operation IDs use camelCase naming convention throughout the HTTP, Console, Events, Client SDK, and Server SDK APIs.
  given: $.paths[*][*].operationId
  name: statsig-operation-ids-camel-case
  severity: warn
- description: All Statsig API operation summaries must use Title Case for readability and consistency across all API specifications.
  given: $.paths[*][*].summary
  name: statsig-summaries-title-case
  severity: warn
- description: Every Statsig API operation must declare at least one tag for proper documentation grouping.
  given: $.paths[*][*]
  name: statsig-tags-required
  severity: error
- description: Log event operations in Statsig APIs require the STATSIG-CLIENT-TIME header for timestamp normalization. Operations that accept events must declare this header parameter.
  given: $.paths['/log_event'][*].parameters[?(@.name == 'STATSIG-CLIENT-TIME')]
  name: statsig-client-time-header
  severity: warn
- description: Console API list operations use limit and page query parameters for pagination. List endpoints should declare these parameters.
  given: $.paths[?(!@ =~ /.*\{.*\}.*/)]..get.parameters[?(@.name == 'limit')]
  name: statsig-pagination-parameters
  severity: hint
- description: The Console API uses STATSIG-API-VERSION header for versioning. Console API operations should declare this optional header parameter.
  given: $.paths[*].get.parameters[?(@.name == 'STATSIG-API-VERSION')]
  name: statsig-api-version-header
  severity: hint
- description: Statsig Console API uses string-type IDs (gate names, config names) as path parameters rather than numeric IDs.
  given: $.paths[*][*].parameters[?(@.name == 'id' && @.in == 'path')]
  name: statsig-console-resource-ids
  severity: warn
- description: Statsig event ingestion endpoints return 202 Accepted (not 200 OK) since events are processed asynchronously.
  given: $.paths['/log_event'][*].responses
  name: statsig-events-202-response
  severity: warn
- description: 'Statsig API event endpoints return a simple {"success": true} response body on success. Responses should follow this consistent pattern.'
  given: $.paths['/log_event'][*].responses['202'].content['application/json'].schema.properties
  name: statsig-success-boolean-response
  severity: hint
rules_file: rules/statsig-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/rules/statsig-rules.yml
severity_counts:
  error: 2
  hint: 3
  info: 0
  warn: 5
slug: statsig-rules
source_filename: statsig-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  statsig-api-key-header:\n    description: >-\n      Statsig APIs require authentication via the statsig-api-key header.\n      All operations must declare this security requirement.\n    message: >-\n      Operations should declare statsig-api-key header authentication.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  statsig-operation-ids-camel-case:\n    description: >-\n      Statsig API operation IDs use camelCase naming convention throughout\n      the HTTP, Console, Events, Client SDK, and Server SDK APIs.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  statsig-summaries-title-case:\n    description: >-\n      All Statsig API operation summaries must use Title Case for\n      readability and consistency across\
  \ all API specifications.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Za-z][a-zA-Z0-9]*)*$\"\n\n  statsig-tags-required:\n    description: >-\n      Every Statsig API operation must declare at least one tag for\n      proper documentation grouping.\n    message: \"Operations must declare at least one tag.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  statsig-client-time-header:\n    description: >-\n      Log event operations in Statsig APIs require the STATSIG-CLIENT-TIME\n      header for timestamp normalization. Operations that accept events\n      must declare this header parameter.\n    message: >-\n      Event logging endpoints must require the STATSIG-CLIENT-TIME header\n      parameter.\n    severity: warn\n    given: \"$.paths['/log_event'][*].parameters[?(@.name\
  \ == 'STATSIG-CLIENT-TIME')]\"\n    then:\n      field: required\n      function: truthy\n\n  statsig-pagination-parameters:\n    description: >-\n      Console API list operations use limit and page query parameters\n      for pagination. List endpoints should declare these parameters.\n    message: >-\n      List operations should include limit and page query parameters\n      for pagination.\n    severity: hint\n    given: \"$.paths[?(!@ =~ /.*\\\\{.*\\\\}.*/)]..get.parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema.maximum\n      function: truthy\n\n  statsig-api-version-header:\n    description: >-\n      The Console API uses STATSIG-API-VERSION header for versioning.\n      Console API operations should declare this optional header parameter.\n    message: >-\n      Console API operations should declare the STATSIG-API-VERSION header\n      parameter.\n    severity: hint\n    given: \"$.paths[*].get.parameters[?(@.name == 'STATSIG-API-VERSION')]\"\n    then:\n   \
  \   field: schema.default\n      function: truthy\n\n  statsig-console-resource-ids:\n    description: >-\n      Statsig Console API uses string-type IDs (gate names, config names)\n      as path parameters rather than numeric IDs.\n    message: >-\n      Path parameter 'id' in Console API paths should be typed as string.\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'id' && @.in == 'path')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  statsig-events-202-response:\n    description: >-\n      Statsig event ingestion endpoints return 202 Accepted (not 200 OK)\n      since events are processed asynchronously.\n    message: >-\n      Event logging operations should return 202 (Accepted) not 200 (OK)\n      since events are processed asynchronously.\n    severity: warn\n    given: \"$.paths['/log_event'][*].responses\"\n    then:\n      field: \"202\"\n      function: truthy\n\n\
  \  statsig-success-boolean-response:\n    description: >-\n      Statsig API event endpoints return a simple {\"success\": true} response\n      body on success. Responses should follow this consistent pattern.\n    message: >-\n      Event endpoint success responses should include a \"success\" boolean\n      property.\n    severity: hint\n    given: \"$.paths['/log_event'][*].responses['202'].content['application/json'].schema.properties\"\n    then:\n      field: success\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/statsig/refs/heads/main/rules/statsig-rules.yml
tags:
- Spectral
- Linting
- API Governance
---
