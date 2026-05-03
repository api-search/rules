---
api_specs:
- filename: sso-saml-openapi.yml
  format: yaml
  label: SAML SSO Authentication API
  slug: saml-authentication
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sso/refs/heads/main/openapi/sso-saml-openapi.yml
- filename: sso-oidc-openapi.yml
  format: yaml
  label: OpenID Connect (OIDC) Authentication API
  slug: oidc-authentication
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sso/refs/heads/main/openapi/sso-oidc-openapi.yml
categories:
- sso
description: Spectral linting rules defining API design standards and conventions for SSO.
layout: rules
name: SSO API Rules
provider_name: SSO
provider_slug: sso
rule_count: 10
rules:
- description: All SSO API operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sso-operation-summaries-title-case
  severity: warn
- description: SSO APIs must define security schemes
  given: $.components
  name: sso-security-scheme-defined
  severity: error
- description: All SSO API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sso-paths-must-have-summary
  severity: warn
- description: SSO API paths should use kebab-case
  given: $.paths[*]~
  name: sso-paths-kebab-case
  severity: warn
- description: All SSO API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sso-operations-must-have-operationid
  severity: error
- description: SSO API operationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sso-operationid-camel-case
  severity: warn
- description: SSO API operations should define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: sso-response-200-or-2xx
  severity: warn
- description: All tags used in operations must be defined in the global tags list
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: sso-tags-must-be-defined
  severity: warn
- description: SSO API specs must include contact information
  given: $.info
  name: sso-info-contact
  severity: warn
- description: SSO API specs must define at least one server
  given: $
  name: sso-servers-defined
  severity: error
rules_file: rules/sso-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sso/refs/heads/main/rules/sso-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: sso-rules
source_filename: sso-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sso-operation-summaries-title-case:\n    description: All SSO API operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  sso-security-scheme-defined:\n    description: SSO APIs must define security schemes\n    message: \"SSO API spec must define at least one security scheme in components/securitySchemes\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  sso-paths-must-have-summary:\n    description: All SSO API operations must have a summary\n    message: \"Operation {{path}} must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function:\
  \ truthy\n\n  sso-paths-kebab-case:\n    description: SSO API paths should use kebab-case\n    message: \"Path segment '{{value}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{][a-z0-9-{}/.]*)*$\"\n\n  sso-operations-must-have-operationid:\n    description: All SSO API operations must have an operationId\n    message: \"Operation {{path}} is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sso-operationid-camel-case:\n    description: SSO API operationIds must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sso-response-200-or-2xx:\n    description:\
  \ SSO API operations should define at least one 2xx response\n    message: \"Operation must define at least one 2xx success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  sso-tags-must-be-defined:\n    description: All tags used in operations must be defined in the global tags list\n    message: \"Tag '{{value}}' is used in an operation but not defined globally\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: truthy\n\n  sso-info-contact:\n    description: SSO API specs must include contact information\n    message: \"SSO API spec must have info.contact defined\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sso-servers-defined:\n    description: SSO API specs must define at least one server\n\
  \    message: \"SSO API spec must define at least one server entry\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sso/refs/heads/main/rules/sso-rules.yml
tags:
- Authentication
- Authorization
- Identity
- OAuth
- OIDC
- SAML
- Security
- Single Sign-On
- SSO
- Spectral
- Linting
- API Governance
---
