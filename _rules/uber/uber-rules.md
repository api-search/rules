---
api_specs:
- filename: uber-riders-openapi.yml
  format: yaml
  label: Uber Riders API
  slug: uber-riders
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-riders-openapi.yml
- filename: uber-drivers-openapi.yml
  format: yaml
  label: Uber Drivers API
  slug: uber-drivers
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-drivers-openapi.yml
- filename: uber-eats-openapi.yml
  format: yaml
  label: Uber Eats API
  slug: uber-eats
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-eats-openapi.yml
- filename: uber-direct-openapi.yml
  format: yaml
  label: Uber Direct API
  slug: uber-direct
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-direct-openapi.yml
- filename: uber-vouchers-openapi.yml
  format: yaml
  label: Uber Vouchers API
  slug: uber-vouchers
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-vouchers-openapi.yml
- filename: uber-businesses-openapi.yml
  format: yaml
  label: Uber for Business API
  slug: uber-businesses
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/openapi/uber-businesses-openapi.yml
categories:
- uber
description: Spectral linting rules defining API design standards and conventions for Uber.
layout: rules
name: Uber API Rules
provider_name: Uber
provider_slug: uber
rule_count: 11
rules:
- description: Operation IDs must use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: uber-operation-id-camel-case
  severity: warn
- description: API paths must use kebab-case segments.
  given: $.paths[*]~
  name: uber-path-kebab-case
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: uber-summary-title-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: uber-has-tags
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: uber-has-operation-id
  severity: error
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: uber-has-description
  severity: warn
- description: Successful GET operations should return a response body schema.
  given: $.paths[*].get.responses.200
  name: uber-200-response-body
  severity: warn
- description: Uber APIs require OAuth 2.0 bearer token authentication.
  given: $.paths[*][get,post,put,patch,delete]
  name: uber-bearer-auth-required
  severity: warn
- description: Uber server URLs should include a version prefix.
  given: $.servers[*].url
  name: uber-version-prefix
  severity: warn
- description: API paths must not have trailing slashes.
  given: $.paths[*]~
  name: uber-no-trailing-slash
  severity: warn
- description: API info block must include title, description, version, and contact.
  given: $.info
  name: uber-required-info-fields
  severity: error
rules_file: rules/uber-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/rules/uber-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 9
slug: uber-rules
source_filename: uber-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Uber API Naming Conventions\n  uber-operation-id-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., createRideRequest, listProducts).\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  uber-path-kebab-case:\n    description: API paths must use kebab-case segments.\n    message: \"Path segment '{{path}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-z0-9-]*(/[a-z0-9][a-z0-9-]*|/\\\\{[a-zA-Z_]+\\\\})*)*$\"\n\n  uber-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  uber-has-tags:\n    description: All operations must have at least one tag.\n    message: Operation is missing tags.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  uber-has-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  uber-has-description:\n    description: All operations must have a description.\n    message: Operation is missing a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  uber-200-response-body:\n    description: Successful GET operations should return a response body schema.\n\
  \    message: GET operation at '{{path}}' should define a response body for 200.\n    severity: warn\n    given: \"$.paths[*].get.responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  uber-bearer-auth-required:\n    description: Uber APIs require OAuth 2.0 bearer token authentication.\n    message: Operation should specify security with BearerAuth.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  uber-version-prefix:\n    description: Uber server URLs should include a version prefix.\n    message: \"Server URL '{{value}}' should include a version path (e.g., /v1, /v1.2).\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://.*uber\\\\.com/v[0-9]\"\n\n  uber-no-trailing-slash:\n    description: API paths must not have trailing\
  \ slashes.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  uber-required-info-fields:\n    description: API info block must include title, description, version, and contact.\n    message: \"Info block is missing required field.\"\n    severity: error\n    given: \"$.info\"\n    then:\n      - field: title\n        function: truthy\n      - field: description\n        function: truthy\n      - field: version\n        function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uber/refs/heads/main/rules/uber-rules.yml
tags:
- Ride-Sharing
- Rides
- Taxis
- Transportation
- Food Delivery
- Delivery
- Logistics
- Spectral
- Linting
- API Governance
---
