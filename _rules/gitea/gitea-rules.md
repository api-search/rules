---
api_specs:
- filename: swagger.v1.json
  format: json
  label: Gitea REST API
  slug: gitea-rest-api
  spec_type: OpenAPI
  url: https://demo.gitea.com/swagger.v1.json
categories:
- gitea
description: Spectral linting rules defining API design standards and conventions for Gitea.
layout: rules
name: Gitea API Rules
provider_name: Gitea
provider_slug: gitea
rule_count: 16
rules:
- description: API contact information must be present.
  given: $.info
  name: gitea-info-contact
  severity: error
- description: API license must be declared (Gitea is MIT).
  given: $.info
  name: gitea-info-license
  severity: warn
- description: Production servers must use HTTPS.
  given: $.servers[*].url
  name: gitea-server-https
  severity: error
- description: Base path must include /api/v1 to match Gitea's documented API surface.
  given: $.servers[*].url
  name: gitea-base-path-versioned
  severity: warn
- description: Security schemes must be declared (Gitea supports BasicAuth, Token, AccessToken, AuthorizationHeaderToken, TOTPHeader, SudoHeader, SudoParam).
  given: $.components.securitySchemes
  name: gitea-auth-required
  severity: error
- description: Every operation must declare a unique operationId (camelCase).
  given: $.paths[*][get,post,put,patch,delete]
  name: gitea-operation-id
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: gitea-operation-id-camelcase
  severity: warn
- description: Every operation must declare at least one tag (admin, repository, issue, organization, user, package, notification, miscellaneous, settings).
  given: $.paths[*][get,post,put,patch,delete]
  name: gitea-operation-tags
  severity: warn
- description: Every operation must include a Title Case summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: gitea-operation-summary
  severity: warn
- description: Operation summaries should be Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: gitea-summary-title-case
  severity: hint
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: gitea-error-responses
  severity: warn
- description: List operations should support page and limit query parameters (Gitea pagination convention).
  given: $.paths[*].get.parameters[?(@.in == 'query')].name
  name: gitea-list-pagination
  severity: hint
- description: Path segments must be lowercase and use snake_case for static segments and {camelCase} for parameters; Gitea uses lowercase REST resources (e.g. /repos, /orgs, /users).
  given: $.paths
  name: gitea-path-naming
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths
  name: gitea-no-trailing-slash
  severity: warn
- description: Definition / schema fields with required arrays should reference real properties only.
  given: $.components.schemas[*]
  name: gitea-schema-required
  severity: warn
- description: Deprecated operations should be flagged with x-deprecated or deprecated:true and have a replacement note in description.
  given: $.paths[*][get,post,put,patch,delete][?(@.deprecated == true)]
  name: gitea-deprecated-marked
  severity: hint
rules_file: rules/gitea-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/gitea/refs/heads/main/rules/gitea-rules.yml
severity_counts:
  error: 4
  hint: 3
  info: 0
  warn: 9
slug: gitea-rules
source_filename: gitea-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for the Gitea REST API.\n# Captures conventions observed in the Gitea Swagger 2.0 / OpenAPI 3.0\n# specification and Gitea's documented best practices.\nrules:\n  gitea-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  gitea-info-license:\n    description: API license must be declared (Gitea is MIT).\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  gitea-server-https:\n    description: Production servers must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  gitea-base-path-versioned:\n    description: Base path must include /api/v1 to match Gitea's documented API surface.\n    severity: warn\n    given: \"$.servers[*].url\"\n   \
  \ then:\n      function: pattern\n      functionOptions:\n        match: \"/api/v1\"\n\n  gitea-auth-required:\n    description: Security schemes must be declared (Gitea supports BasicAuth, Token, AccessToken, AuthorizationHeaderToken, TOTPHeader, SudoHeader, SudoParam).\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  gitea-operation-id:\n    description: Every operation must declare a unique operationId (camelCase).\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  gitea-operation-id-camelcase:\n    description: operationId must be camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  gitea-operation-tags:\n    description: Every operation must declare at least one tag (admin, repository, issue,\
  \ organization, user, package, notification, miscellaneous, settings).\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  gitea-operation-summary:\n    description: Every operation must include a Title Case summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  gitea-summary-title-case:\n    description: Operation summaries should be Title Case.\n    severity: hint\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  gitea-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n     \
  \ functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [ \"400\" ]\n            - required: [ \"401\" ]\n            - required: [ \"403\" ]\n            - required: [ \"404\" ]\n            - required: [ \"422\" ]\n\n  gitea-list-pagination:\n    description: List operations should support page and limit query parameters (Gitea pagination convention).\n    severity: hint\n    given: \"$.paths[*].get.parameters[?(@.in == 'query')].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - limit\n          - q\n          - state\n          - type\n          - sort\n          - order\n          - since\n          - before\n          - owner\n          - repo\n          - org\n          - user\n          - team\n          - kind\n          - mode\n          - access_token\n          - sudo\n          - private\n          - includeDesc\n          - all\n          - tags\n          -\
  \ exclusive\n          - include\n          - milestones\n          - keyword\n          - first_only\n\n  gitea-path-naming:\n    description: Path segments must be lowercase and use snake_case for static segments and {camelCase} for parameters; Gitea uses lowercase REST resources (e.g. /repos, /orgs, /users).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/.*\"\n\n  gitea-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  gitea-schema-required:\n    description: Definition / schema fields with required arrays should reference real properties only.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      function: truthy\n      field: type\n\n  gitea-deprecated-marked:\n    description: Deprecated operations should be flagged with\
  \ x-deprecated or deprecated:true and have a replacement note in description.\n    severity: hint\n    given: \"$.paths[*][get,post,put,patch,delete][?(@.deprecated == true)]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/gitea/refs/heads/main/rules/gitea-rules.yml
tags:
- Git
- Source Control
- DevOps
- CI/CD
- Code Hosting
- Open Source
- Self Hosted
- Package Registry
- Issue Tracking
- Pull Requests
- Spectral
- Linting
- API Governance
---
