---
api_specs:
- filename: sonatype-nexus-repository-openapi.yml
  format: yaml
  label: Nexus Repository API
  slug: nexus-repository-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sonatype-nexus/refs/heads/main/openapi/sonatype-nexus-repository-openapi.yml
categories:
- nexus
description: Spectral linting rules defining API design standards and conventions for Sonatype Nexus.
layout: rules
name: Sonatype Nexus API Rules
provider_name: Sonatype Nexus
provider_slug: sonatype-nexus
rule_count: 9
rules:
- description: ''
  given: $.paths[*]~
  name: nexus-path-version-prefix
  severity: warn
- description: ''
  given: $.paths[*][*].summary
  name: nexus-operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: nexus-operation-id-required
  severity: error
- description: ''
  given: $.paths[*]~
  name: nexus-repository-path-param-naming
  severity: warn
- description: ''
  given: $.paths[*][get,post,put,delete,patch]
  name: nexus-operation-tags-required
  severity: warn
- description: ''
  given: $.components.securitySchemes
  name: nexus-security-schemes-defined
  severity: error
- description: ''
  given: $.paths[*][get,post,put,delete,patch].responses
  name: nexus-success-response-required
  severity: warn
- description: ''
  given: $.info
  name: nexus-info-contact-required
  severity: warn
- description: ''
  given: $.paths[*]~
  name: nexus-no-trailing-slash
  severity: warn
rules_file: rules/sonatype-nexus-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sonatype-nexus/refs/heads/main/rules/sonatype-nexus-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 7
slug: sonatype-nexus-rules
source_filename: sonatype-nexus-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Nexus Repository API uses /v1/ and /beta/ versioning prefixes\n  nexus-path-version-prefix:\n    message: \"Paths must start with /v1/ or /beta/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(v1|beta)/\"\n\n  # All operation summaries should use Title Case\n  nexus-operation-summary-title-case:\n    message: \"Operation summaries should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # All operations should have an operationId\n  nexus-operation-id-required:\n    message: \"Operations must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Repository name path parameters should use {repositoryName} or {name}\n  nexus-repository-path-param-naming:\n\
  \    message: \"Repository path parameters should be {repositoryName} or {name}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\{repo\\\\}|\\\\{repository\\\\}|\\\\{repoName\\\\}\"\n\n  # Operations must have at least one tag\n  nexus-operation-tags-required:\n    message: \"Operations must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # API must define security schemes\n  nexus-security-schemes-defined:\n    message: \"API must define security schemes (BasicAuth)\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  # Responses must document at least a 2xx response\n  nexus-success-response-required:\n    message: \"Operations must document at least one success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  # Info must have contact\n  nexus-info-contact-required:\n    message: \"API info must have a contact field\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # No trailing slashes on paths\n  nexus-no-trailing-slash:\n    message: \"Paths must not end with a trailing slash\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sonatype-nexus/refs/heads/main/rules/sonatype-nexus-rules.yml
tags:
- Artifact Management
- DevOps
- Package Management
- Repository
- Maven
- npm
- Docker
- Software Supply Chain
- Spectral
- Linting
- API Governance
---
