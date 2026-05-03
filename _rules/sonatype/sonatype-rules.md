---
api_specs:
- filename: sonatype-lifecycle-openapi.yml
  format: yaml
  label: Sonatype Lifecycle API
  slug: sonatype-lifecycle-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sonatype/refs/heads/main/openapi/sonatype-lifecycle-openapi.yml
categories:
- sonatype
description: Spectral linting rules defining API design standards and conventions for Sonatype.
layout: rules
name: Sonatype API Rules
provider_name: Sonatype
provider_slug: sonatype
rule_count: 8
rules:
- description: ''
  given: $.paths[*]~
  name: sonatype-path-version-prefix
  severity: warn
- description: ''
  given: $.paths[*][*].summary
  name: sonatype-operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: sonatype-operation-id-required
  severity: error
- description: ''
  given: $.paths[*]~
  name: sonatype-owner-type-param-naming
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: sonatype-operation-tags-required
  severity: warn
- description: ''
  given: $.components.securitySchemes
  name: sonatype-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,delete,patch].responses
  name: sonatype-success-response-required
  severity: warn
- description: ''
  given: $.paths[*]~
  name: sonatype-no-trailing-slash
  severity: warn
rules_file: rules/sonatype-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sonatype/refs/heads/main/rules/sonatype-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: sonatype-rules
source_filename: sonatype-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Sonatype Lifecycle API uses /api/v2/ versioning prefix\n  sonatype-path-version-prefix:\n    message: \"Paths must start with /api/v2/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v2/\"\n\n  # All operation summaries should use Title Case\n  sonatype-operation-summary-title-case:\n    message: \"Operation summaries should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations should have an operationId\n  sonatype-operation-id-required:\n    message: \"Operations must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Owner type path parameters should follow {ownerType} convention\n  sonatype-owner-type-param-naming:\n\
  \    message: \"Owner type parameters should use {ownerType}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\{owner_type\\\\}|\\\\{ownertype\\\\}\"\n\n  # Operations must have at least one tag\n  sonatype-operation-tags-required:\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # API must define security schemes\n  sonatype-security-schemes-defined:\n    message: \"API must define security schemes\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  # Responses must document at least a 2xx response\n  sonatype-success-response-required:\n    message: \"Operations must document at least one success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n     \
  \ function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # No trailing slashes on paths\n  sonatype-no-trailing-slash:\n    message: \"Paths must not end with a trailing slash\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sonatype/refs/heads/main/rules/sonatype-rules.yml
tags:
- Software Supply Chain
- Security
- Vulnerability Management
- SBOM
- Software Composition Analysis
- DevSecOps
- Spectral
- Linting
- API Governance
---
