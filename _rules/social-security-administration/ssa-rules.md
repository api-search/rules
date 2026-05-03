---
api_specs:
- filename: ssa-field-office-openapi.yml
  format: yaml
  label: SSA Field Office Address API
  slug: field-office-address-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/social-security-administration/refs/heads/main/openapi/ssa-field-office-openapi.yml
- filename: ssa-resident-station-openapi.yml
  format: yaml
  label: SSA Resident Station Address API
  slug: resident-station-address-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/social-security-administration/refs/heads/main/openapi/ssa-resident-station-openapi.yml
categories:
- ssa
description: Spectral linting rules defining API design standards and conventions for Social Security Administration.
layout: rules
name: Social Security Administration API Rules
provider_name: Social Security Administration
provider_slug: social-security-administration
rule_count: 8
rules:
- description: SSA public data APIs do not require authentication
  given: $.security
  name: ssa-no-authentication
  severity: info
- description: ArcGIS query endpoints should document the required where parameter
  given: $.paths.*.get.parameters[?(@.name == 'where')]
  name: ssa-arcgis-query-where-required
  severity: error
- description: ArcGIS endpoints should document the f (format) parameter
  given: $.paths.*.*.parameters
  name: ssa-arcgis-format-parameter
  severity: warn
- description: Government APIs must document public domain licensing
  given: $.info.license
  name: ssa-government-license-documented
  severity: error
- description: Government APIs must provide contact information
  given: $.info.contact
  name: ssa-contact-info-required
  severity: error
- description: All operations must have tags
  given: $.paths.*.*
  name: ssa-tags-required
  severity: error
- description: Responses should define a schema for data consumers
  given: $.paths.*.*.responses.*.content.*.schema
  name: ssa-response-schema-defined
  severity: warn
- description: URL path segments should use kebab-case
  given: $.paths
  name: ssa-path-kebab-case
  severity: warn
rules_file: rules/ssa-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/social-security-administration/refs/heads/main/rules/ssa-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 3
slug: ssa-rules
source_filename: ssa-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ssa-no-authentication:\n    description: SSA public data APIs do not require authentication\n    message: \"SSA public location APIs should not require authentication — they serve public government data.\"\n    severity: info\n    given: \"$.security\"\n    then:\n      function: falsy\n\n  ssa-arcgis-query-where-required:\n    description: ArcGIS query endpoints should document the required where parameter\n    message: \"ArcGIS query endpoints must document the 'where' parameter for SQL filtering.\"\n    severity: error\n    given: \"$.paths.*.get.parameters[?(@.name == 'where')]\"\n    then:\n      field: required\n      function: truthy\n\n  ssa-arcgis-format-parameter:\n    description: ArcGIS endpoints should document the f (format) parameter\n    message: \"ArcGIS REST endpoints should document the 'f' parameter for response format selection.\"\n    severity: warn\n    given: \"$.paths.*.*.parameters\"\n    then:\n      function: truthy\n\
  \n  ssa-government-license-documented:\n    description: Government APIs must document public domain licensing\n    message: \"Government APIs must document their license as public domain or U.S. Government Work.\"\n    severity: error\n    given: \"$.info.license\"\n    then:\n      field: name\n      function: truthy\n\n  ssa-contact-info-required:\n    description: Government APIs must provide contact information\n    message: \"Government API specifications must include contact information for the agency.\"\n    severity: error\n    given: \"$.info.contact\"\n    then:\n      field: url\n      function: truthy\n\n  ssa-tags-required:\n    description: All operations must have tags\n    message: \"All SSA API operations must include descriptive tags.\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  ssa-response-schema-defined:\n    description: Responses should define a schema for data consumers\n    message: \"API responses\
  \ should define a schema to help developers understand the data structure.\"\n    severity: warn\n    given: \"$.paths.*.*.responses.*.content.*.schema\"\n    then:\n      function: truthy\n\n  ssa-path-kebab-case:\n    description: URL path segments should use kebab-case\n    message: \"Path segments should use kebab-case (lowercase with hyphens).\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*/?$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/social-security-administration/refs/heads/main/rules/ssa-rules.yml
tags:
- Federal Government
- Social Security
- Government API
- Open Data
- OASDI
- Disability Benefits
- Retirement Benefits
- Spectral
- Linting
- API Governance
---
