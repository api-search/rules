---
api_specs:
- filename: steelcase-roomwizard-api-openapi.yml
  format: yaml
  label: Steelcase RoomWizard API
  slug: roomwizard-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/steelcase/refs/heads/main/openapi/steelcase-roomwizard-api-openapi.yml
categories:
- steelcase
description: Spectral linting rules defining API design standards and conventions for Steelcase.
layout: rules
name: Steelcase API Rules
provider_name: Steelcase
provider_slug: steelcase
rule_count: 8
rules:
- description: Steelcase RoomWizard API operation IDs use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: steelcase-operation-ids-camel-case
  severity: warn
- description: All Steelcase RoomWizard API operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: steelcase-summaries-title-case
  severity: warn
- description: Every Steelcase API operation must have at least one tag.
  given: $.paths[*][*]
  name: steelcase-tags-required
  severity: error
- description: Booking creation requests must include room_id, subject, start_time, and end_time as required fields.
  given: $.components.schemas.BookingCreate
  name: steelcase-booking-required-fields
  severity: error
- description: All date and time properties in the Steelcase API should use ISO 8601 date-time format.
  given: $.components.schemas[*].properties[?(@ =~ /.*_time$|.*_at$/)]
  name: steelcase-date-time-format
  severity: warn
- description: Steelcase RoomWizard API properties use snake_case naming convention (e.g., room_id, start_time, booking_id).
  given: $.components.schemas[*].properties
  name: steelcase-snake-case-properties
  severity: warn
- description: Booking status should use the standard Steelcase status values.
  given: $.components.schemas.Booking.properties.status.enum
  name: steelcase-status-enum
  severity: warn
- description: Steelcase API responses should return application/json content type.
  given: $.paths[*][*].responses['200'].content
  name: steelcase-responses-json
  severity: warn
rules_file: rules/steelcase-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/steelcase/refs/heads/main/rules/steelcase-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: steelcase-rules
source_filename: steelcase-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  steelcase-operation-ids-camel-case:\n    description: >-\n      Steelcase RoomWizard API operation IDs use camelCase naming convention.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  steelcase-summaries-title-case:\n    description: >-\n      All Steelcase RoomWizard API operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should be in Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  steelcase-tags-required:\n    description: >-\n      Every Steelcase API operation must have at least one tag.\n    message: \"Operations must declare at least one tag.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n  \
  \  then:\n      field: tags\n      function: truthy\n\n  steelcase-booking-required-fields:\n    description: >-\n      Booking creation requests must include room_id, subject, start_time,\n      and end_time as required fields.\n    message: >-\n      BookingCreate schema must require room_id, subject, start_time,\n      and end_time fields.\n    severity: error\n    given: \"$.components.schemas.BookingCreate\"\n    then:\n      field: required\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: string\n            enum:\n              - room_id\n              - subject\n              - start_time\n              - end_time\n\n  steelcase-date-time-format:\n    description: >-\n      All date and time properties in the Steelcase API should use\n      ISO 8601 date-time format.\n    message: >-\n      Date/time fields should declare format: date-time for consistency.\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@\
  \ =~ /.*_time$|.*_at$/)]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n          - date\n\n  steelcase-snake-case-properties:\n    description: >-\n      Steelcase RoomWizard API properties use snake_case naming convention\n      (e.g., room_id, start_time, booking_id).\n    message: \"Property '{{property}}' should use snake_case naming.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          propertyNames:\n            pattern: \"^[a-z][a-z0-9]*(_[a-z0-9]+)*$\"\n\n  steelcase-status-enum:\n    description: >-\n      Booking status should use the standard Steelcase status values.\n    message: >-\n      Booking status must be one of: confirmed, cancelled, in-progress,\n      completed.\n    severity: warn\n    given: \"$.components.schemas.Booking.properties.status.enum\"\n    then:\n\
  \      function: truthy\n\n  steelcase-responses-json:\n    description: >-\n      Steelcase API responses should return application/json content type.\n    message: \"Success responses must include application/json content.\"\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/steelcase/refs/heads/main/rules/steelcase-rules.yml
tags:
- Office Furniture
- Workplace
- Room Scheduling
- Facilities Management
- IoT
- Smart Office
- Spectral
- Linting
- API Governance
---
