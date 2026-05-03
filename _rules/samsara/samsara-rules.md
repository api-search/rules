---
api_specs:
- filename: samsara-openapi.yml
  format: yaml
  label: Samsara API
  slug: samsara
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/samsara/refs/heads/main/openapi/samsara-openapi.yml
categories:
- samsara
description: Spectral linting rules defining API design standards and conventions for Samsara.
layout: rules
name: Samsara API Rules
provider_name: Samsara
provider_slug: samsara
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: samsara-operation-summary-title-case
  severity: warn
- description: OperationIds must use lowerCamelCase
  given: $.paths[*][*].operationId
  name: samsara-operation-id-camel-case
  severity: warn
- description: All tags used in operations must be defined in the global tags list
  given: $.paths[*][*].tags[*]
  name: samsara-tags-defined
  severity: warn
- description: All 200 responses should have a schema defined
  given: $.paths[*][*].responses['200'].content[*]
  name: samsara-response-200-schema
  severity: warn
- description: Operations should use the AccessTokenHeader security scheme
  given: $.paths[*][*]
  name: samsara-bearer-auth-used
  severity: info
- description: List operations should support cursor-based pagination with 'after' parameter
  given: $.paths[?(!@property.match(/\{.*\}/))].get.parameters[*]
  name: samsara-pagination-cursor-pattern
  severity: info
- description: API paths must not end with a trailing slash
  given: $.paths
  name: samsara-no-trailing-slash
  severity: error
- description: Path segments must use kebab-case or camelCase (Samsara convention)
  given: $.paths
  name: samsara-path-kebab-case
  severity: info
- description: Resources that support external IDs should document them
  given: $.paths[*][*].description
  name: samsara-external-id-support
  severity: info
rules_file: rules/samsara-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/samsara/refs/heads/main/rules/samsara-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 4
  warn: 4
slug: samsara-rules
source_filename: samsara-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\nrules:\n  # Samsara API Conventions\n\n  samsara-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\[(?:beta|preview|legacy)\\\\] )?[A-Z]\"\n\n  samsara-operation-id-camel-case:\n    description: OperationIds must use lowerCamelCase\n    message: \"OperationId '{{value}}' should use lowerCamelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  samsara-tags-defined:\n    description: All tags used in operations must be defined in the global tags list\n    message: \"Tag '{{value}}' is used but not defined in global tags\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n  \
  \    function: enumeration\n      functionOptions:\n        values:\n          - Addresses\n          - Assets\n          - Attributes\n          - Camera Media\n          - Carrier Proposed Assignments\n          - Contacts\n          - Documents\n          - Drivers\n          - Driver Vehicle Assignments\n          - Equipment\n          - Hours of Service\n          - Industrial\n          - Maintenance\n          - Messages\n          - Organization Info\n          - Routes\n          - Safety\n          - Sensors\n          - Tachograph (EU Only)\n          - Tags\n          - Trailer Assignments\n          - Trips\n          - Users\n          - Vehicles\n          - Vehicle Driver Assignments\n          - Vehicle Stats\n          - Vehicle Locations\n          - Beta APIs\n          - Preview APIs\n          - Legacy APIs\n\n  samsara-response-200-schema:\n    description: All 200 responses should have a schema defined\n    message: \"200 response should define a schema\"\n   \
  \ severity: warn\n    given: \"$.paths[*][*].responses['200'].content[*]\"\n    then:\n      field: schema\n      function: defined\n\n  samsara-bearer-auth-used:\n    description: Operations should use the AccessTokenHeader security scheme\n    message: \"Operation should use AccessTokenHeader security\"\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  samsara-pagination-cursor-pattern:\n    description: List operations should support cursor-based pagination with 'after' parameter\n    message: \"List operations (GET on collection) should support 'after' pagination parameter\"\n    severity: info\n    given: \"$.paths[?(!@property.match(/\\\\{.*\\\\}/))].get.parameters[*]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^(limit|after|before|tagIds|parentTagIds|updatedAfterTime|createdAfterTime)$\"\n\n  samsara-no-trailing-slash:\n    description: API paths must not end with\
  \ a trailing slash\n    message: \"Path '{{property}}' must not end with a trailing slash\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  samsara-path-kebab-case:\n    description: Path segments must use kebab-case or camelCase (Samsara convention)\n    message: \"Path segment should use kebab-case\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9\\\\-_\\\\{\\\\}]+)+$\"\n\n  samsara-external-id-support:\n    description: Resources that support external IDs should document them\n    message: \"External IDs should be documented in the description\"\n    severity: info\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/samsara/refs/heads/main/rules/samsara-rules.yml
tags:
- Asset Tracking
- Connected Operations
- ELD
- Fleet Management
- GPS Tracking
- IoT
- Logistics
- Safety
- Telematics
- Transportation
- Spectral
- Linting
- API Governance
---
