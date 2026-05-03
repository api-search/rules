---
api_specs:
- filename: science-museum-group-collection-openapi.yml
  format: yaml
  label: Science Museum Group Collection API
  slug: collection-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/science-museum-group/refs/heads/main/openapi/science-museum-group-collection-openapi.yml
categories:
- smg
description: Spectral linting rules defining API design standards and conventions for Science Museum Group.
layout: rules
name: Science Museum Group API Rules
provider_name: Science Museum Group
provider_slug: science-museum-group
rule_count: 10
rules:
- description: Science Museum Group API responses must use the JSONAPI content type application/vnd.api+json
  given: $.paths.*.*.responses.*.content
  name: smg-jsonapi-content-type
  severity: warn
- description: All search endpoints must support page[number] and page[size] parameters
  given: $.paths[?(@property.startsWith('/search'))].get.parameters[*].name
  name: smg-search-requires-pagination
  severity: warn
- description: Operation IDs must use camelCase naming
  given: $.paths.*.*.operationId
  name: smg-operation-id-camel-case
  severity: warn
- description: API paths must use kebab-case
  given: $.paths[*]~
  name: smg-path-kebab-case
  severity: warn
- description: All API operations must have a description
  given: $.paths.*.*
  name: smg-operation-description-required
  severity: warn
- description: All API operations must be tagged
  given: $.paths.*.*
  name: smg-operation-tags-required
  severity: warn
- description: Path parameters declared in parameters must appear in the path
  given: $.paths.*.*.parameters[?(@.in == 'path')].name
  name: smg-path-params-used
  severity: error
- description: Endpoints that retrieve a single resource by ID must define a 404 response
  given: $.paths.*[?(@property == 'get')].responses
  name: smg-single-resource-has-404
  severity: warn
- description: APIs must use OpenAPI 3.x specification
  given: $.openapi
  name: smg-openapi-version
  severity: error
- description: API specification must define at least one server URL
  given: $
  name: smg-servers-required
  severity: error
rules_file: rules/science-museum-group-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/science-museum-group/refs/heads/main/rules/science-museum-group-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: science-museum-group-rules
source_filename: science-museum-group-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Science Museum Group Collection API Conventions\n\n  # Enforce JSONAPI content type for all responses\n  smg-jsonapi-content-type:\n    description: Science Museum Group API responses must use the JSONAPI content type application/vnd.api+json\n    message: Response content type must be application/vnd.api+json for JSONAPI compliance\n    severity: warn\n    given: $.paths.*.*.responses.*.content\n    then:\n      field: \"@key\"\n      function: enumeration\n      functionOptions:\n        values:\n          - application/vnd.api+json\n\n  # Enforce pagination parameters on search endpoints\n  smg-search-requires-pagination:\n    description: All search endpoints must support page[number] and page[size] parameters\n    message: Search endpoints should include pagination parameters (page[number], page[size])\n    severity: warn\n    given: $.paths[?(@property.startsWith('/search'))].get.parameters[*].name\n    then:\n      function: enumeration\n\
  \      functionOptions:\n        values:\n          - q\n          - random\n          - page[number]\n          - page[size]\n          - date[from]\n          - date[to]\n          - places\n          - images\n          - type\n          - makers\n          - people\n          - categories\n          - museum\n          - on_display\n          - location\n          - birth[place]\n          - birth[date]\n          - death[date]\n          - occupation\n          - archive\n\n  # Enforce operation IDs follow camelCase convention\n  smg-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: Operation ID {{value}} must use camelCase\n    severity: warn\n    given: $.paths.*.*.operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Enforce all paths use kebab-case\n  smg-path-kebab-case:\n    description: API paths must use kebab-case\n    message: Path {{value}} must use kebab-case\
  \ (lowercase letters and hyphens only)\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9-{}]+)+$\"\n\n  # Require description on all operations\n  smg-operation-description-required:\n    description: All API operations must have a description\n    message: Operation at {{path}} is missing a description\n    severity: warn\n    given: $.paths.*.*\n    then:\n      field: description\n      function: truthy\n\n  # Require tags on all operations\n  smg-operation-tags-required:\n    description: All API operations must be tagged\n    message: Operation at {{path}} is missing tags\n    severity: warn\n    given: $.paths.*.*\n    then:\n      field: tags\n      function: truthy\n\n  # Enforce path parameters are referenced in the path\n  smg-path-params-used:\n    description: Path parameters declared in parameters must appear in the path\n    message: Parameter {{value}} declared as path parameter but not\
  \ found in path\n    severity: error\n    given: $.paths.*.*.parameters[?(@.in == 'path')].name\n    then:\n      function: defined\n\n  # Enforce 404 response for GET single resource endpoints\n  smg-single-resource-has-404:\n    description: Endpoints that retrieve a single resource by ID must define a 404 response\n    message: Single-resource GET endpoint at {{path}} must include a 404 response\n    severity: warn\n    given: $.paths.*[?(@property == 'get')].responses\n    then:\n      field: \"404\"\n      function: defined\n\n  # Require OpenAPI version 3.x\n  smg-openapi-version:\n    description: APIs must use OpenAPI 3.x specification\n    message: API spec must use OpenAPI version 3.x\n    severity: error\n    given: $.openapi\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # Require server URL definition\n  smg-servers-required:\n    description: API specification must define at least one server URL\n    message: API spec must include\
  \ servers definition\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/science-museum-group/refs/heads/main/rules/science-museum-group-rules.yml
tags:
- Museums
- Collections
- Cultural Heritage
- Open Data
- Science
- Technology
- United Kingdom
- Spectral
- Linting
- API Governance
---
