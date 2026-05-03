---
api_specs:
- filename: spring-security-oauth2-openapi.yml
  format: yaml
  label: Spring Security OAuth2 API
  slug: spring-security-oauth2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-security/refs/heads/main/openapi/spring-security-oauth2-openapi.yml
- filename: spring-authorization-server-openapi.yml
  format: yaml
  label: Spring Authorization Server API
  slug: spring-authorization-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spring-security/refs/heads/main/openapi/spring-authorization-server-openapi.yml
categories:
- spring
description: Spectral linting rules defining API design standards and conventions for Spring Security.
layout: rules
name: Spring Security API Rules
provider_name: Spring Security
provider_slug: spring-security
rule_count: 7
rules:
- description: All operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-security-operation-id
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: spring-security-tags-required
  severity: warn
- description: Summaries must use Title Case
  given: $.paths[*][*].summary
  name: spring-security-summary-title-case
  severity: warn
- description: OAuth2 token endpoints must define error response schemas
  given: $.paths[/oauth2/token,/oauth2/introspect].post
  name: spring-security-oauth2-error-responses
  severity: warn
- description: API should define security schemes
  given: $.components
  name: spring-security-security-schemes
  severity: error
- description: Bearer auth scheme should specify bearerFormat
  given: $.components.securitySchemes[*][?(@.scheme == 'bearer')]
  name: spring-security-bearer-format
  severity: info
- description: Sensitive OAuth2 endpoints must have descriptions
  given: $.paths[/oauth2/token,/oauth2/introspect,/oauth2/revoke,/oauth2/authorize][*]
  name: spring-security-sensitive-endpoints-documented
  severity: error
rules_file: rules/spring-security-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spring-security/refs/heads/main/rules/spring-security-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: spring-security-rules
source_filename: spring-security-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spring-security-operation-id:\n    description: All operations must have operationId\n    message: \"Missing operationId at {{path}}\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spring-security-tags-required:\n    description: All operations must have tags\n    message: \"Operation at {{path}} must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spring-security-summary-title-case:\n    description: Summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  spring-security-oauth2-error-responses:\n    description: OAuth2 token endpoints must define error response schemas\n\
  \    message: \"Token endpoint should define 400 error response at {{path}}\"\n    severity: warn\n    given: \"$.paths[/oauth2/token,/oauth2/introspect].post\"\n    then:\n      field: \"responses.400\"\n      function: truthy\n\n  spring-security-security-schemes:\n    description: API should define security schemes\n    message: \"API must define securitySchemes in components\"\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  spring-security-bearer-format:\n    description: Bearer auth scheme should specify bearerFormat\n    message: \"Bearer security scheme should specify bearerFormat: JWT\"\n    severity: info\n    given: \"$.components.securitySchemes[*][?(@.scheme == 'bearer')]\"\n    then:\n      field: bearerFormat\n      function: truthy\n\n  spring-security-sensitive-endpoints-documented:\n    description: Sensitive OAuth2 endpoints must have descriptions\n    message: \"OAuth2 endpoint at {{path}} must have\
  \ description\"\n    severity: error\n    given: \"$.paths[/oauth2/token,/oauth2/introspect,/oauth2/revoke,/oauth2/authorize][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spring-security/refs/heads/main/rules/spring-security-rules.yml
tags:
- Authentication
- Authorization
- Java
- JWT
- OAuth2
- OpenID Connect
- SAML
- Security
- Spring Framework
- Spectral
- Linting
- API Governance
---
