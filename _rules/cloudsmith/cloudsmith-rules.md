---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Cloudsmith API (v1)
  slug: v1
  spec_type: OpenAPI
  url: https://api.cloudsmith.io/?format=openapi
categories:
- cloudsmith
description: Spectral linting rules defining API design standards and conventions for Cloudsmith.
layout: rules
name: Cloudsmith API Rules
provider_name: Cloudsmith
provider_slug: cloudsmith
rule_count: 14
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudsmith-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudsmith-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudsmith-server-https
  severity: error
- description: Cloudsmith APIs must be served from api.cloudsmith.io.
  given: $.servers[*].url
  name: cloudsmith-host
  severity: warn
- description: A security scheme must be declared (token-based apiKey).
  given: $.components.securitySchemes
  name: cloudsmith-auth-required
  severity: error
- description: API key descriptions should mention the "token" Authorization prefix.
  given: $.components.securitySchemes[*]
  name: cloudsmith-token-prefix
  severity: info
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudsmith-operation-id
  severity: error
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudsmith-operation-summary
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudsmith-operation-tags
  severity: warn
- description: Operations should use known Cloudsmith tag groups.
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: cloudsmith-known-tags
  severity: info
- description: List endpoints should support page/page_size pagination params.
  given: $.paths[?(@property.match(/\/$/))].get.parameters[*].name
  name: cloudsmith-pagination
  severity: info
- description: Owner-scoped paths should declare the {owner} path param.
  given: $.paths[?(@property.match(/\{owner\}/))][*].parameters[?(@.in == 'path')].name
  name: cloudsmith-owner-param
  severity: info
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudsmith-error-responses
  severity: warn
- description: Rate-limited endpoints should document a 429 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: cloudsmith-rate-limit
  severity: info
rules_file: rules/cloudsmith-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudsmith/refs/heads/main/rules/cloudsmith-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 5
  warn: 5
slug: cloudsmith-rules
source_filename: cloudsmith-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for the Cloudsmith API (v1).\n# Validates Cloudsmith conventions: api.cloudsmith.io host, \"token\"\n# Authorization scheme, page/page_size pagination, owner/repo path\n# parameters, and JSON content types.\nrules:\n  cloudsmith-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cloudsmith-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cloudsmith-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cloudsmith-host:\n    description: Cloudsmith APIs must be served from api.cloudsmith.io.\n    severity: warn\n    given: \"\
  $.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"api\\\\.cloudsmith\\\\.io\"\n\n  cloudsmith-auth-required:\n    description: A security scheme must be declared (token-based apiKey).\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  cloudsmith-token-prefix:\n    description: API key descriptions should mention the \"token\" Authorization prefix.\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: description\n      function: pattern\n      functionOptions:\n        match: \"(?i)token\"\n\n  cloudsmith-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cloudsmith-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given:\
  \ \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cloudsmith-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cloudsmith-known-tags:\n    description: Operations should use known Cloudsmith tag groups.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - audit-log\n          - badges\n          - broadcasts\n          - bulk-action\n          - distros\n          - entitlements\n          - files\n          - formats\n          - metrics\n          - namespaces\n          - orgs\n          - packages\n          - quota\n          - rates\n          - recycle-bin\n\
  \          - repos\n          - status\n          - storage-regions\n          - user\n          - users\n          - vulnerabilities\n          - webhooks\n\n  cloudsmith-pagination:\n    description: List endpoints should support page/page_size pagination params.\n    severity: info\n    given: \"$.paths[?(@property.match(/\\\\/$/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - page_size\n          - query\n          - sort\n          - search\n\n  cloudsmith-owner-param:\n    description: Owner-scoped paths should declare the {owner} path param.\n    severity: info\n    given: \"$.paths[?(@property.match(/\\\\{owner\\\\}/))][*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - owner\n          - repo\n          - identifier\n          - slug\n          - org\n          - package\n          - format\n\n  cloudsmith-error-responses:\n\
  \    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n\n  cloudsmith-rate-limit:\n    description: Rate-limited endpoints should document a 429 response.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"429\"]\n            - required: [\"200\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudsmith/refs/heads/main/rules/cloudsmith-rules.yml
tags:
- Artifact Management
- DevOps
- DevSecOps
- Distribution
- Package Management
- Registry
- Repository
- Software Supply Chain
- Universal
- Vulnerability Scanning
- Spectral
- Linting
- API Governance
---
