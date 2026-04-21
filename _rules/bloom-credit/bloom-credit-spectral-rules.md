---
categories:
- bloom
description: Spectral linting rules defining API design standards and conventions for Bloom Credit.
layout: rules
name: Bloom Credit API Rules
provider_name: Bloom Credit
provider_slug: bloom-credit
rule_count: 30
rules:
- description: API must have a title
  given: $.info
  name: bloom-credit-info-title
  severity: error
- description: API must have a description
  given: $.info
  name: bloom-credit-info-description
  severity: error
- description: API must have a version
  given: $.info
  name: bloom-credit-info-version
  severity: error
- description: API must have contact information
  given: $.info
  name: bloom-credit-info-contact
  severity: warn
- description: API must have at least one server defined
  given: $
  name: bloom-credit-servers-exist
  severity: error
- description: All servers must use HTTPS
  given: $.servers[*]
  name: bloom-credit-server-https
  severity: error
- description: Each server must have a description
  given: $.servers[*]
  name: bloom-credit-server-description
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: bloom-credit-path-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: bloom-credit-path-no-trailing-slash
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-id-exists
  severity: error
- description: OperationId must use kebab-case
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-id-kebab-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-summary-exists
  severity: error
- description: Operation summaries must start with Bloom Credit
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-summary-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-description-exists
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: bloom-credit-operation-tags
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: bloom-credit-parameter-description
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][*].parameters[*]
  name: bloom-credit-parameter-schema
  severity: error
- description: Operations must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: bloom-credit-response-success-exists
  severity: error
- description: Success responses must have a content schema
  given: $.paths[*][*].responses[200,201].content[*]
  name: bloom-credit-response-schema-exists
  severity: warn
- description: Responses should include examples
  given: $.paths[*][*].responses[200,201].content[*]
  name: bloom-credit-response-examples
  severity: warn
- description: API must define security schemes
  given: $.components
  name: bloom-credit-security-scheme-defined
  severity: error
- description: API should have global security defined
  given: $
  name: bloom-credit-global-security
  severity: warn
- description: API should use API key authentication via X-API-Key header
  given: $.components.securitySchemes[*]
  name: bloom-credit-apikey-auth
  severity: info
- description: All schema objects must have a type
  given: $.components.schemas[*]
  name: bloom-credit-schema-type
  severity: warn
- description: All schema components must have a description
  given: $.components.schemas[*]
  name: bloom-credit-schema-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: bloom-credit-property-description
  severity: info
- description: Consumer endpoints should be nested under /consumers/{consumer_id}
  given: $.paths[/consumers/{consumer_id}*]~
  name: bloom-credit-consumer-id-path
  severity: info
- description: Bureau fields should use valid bureau names
  given: $.components.schemas[*].properties.bureau.enum
  name: bloom-credit-bureau-enum
  severity: info
- description: Credit score schemas should define min/max range
  given: $.components.schemas.CreditScore.properties.score
  name: bloom-credit-score-range
  severity: info
- description: API should have a sandbox server for testing
  given: $.servers
  name: bloom-credit-sandbox-server
  severity: warn
rules_file: rules/bloom-credit-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bloom-credit/refs/heads/main/rules/bloom-credit-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 5
  warn: 14
slug: bloom-credit-spectral-rules
tags:
- Credit Bureau
- Credit Reports
- Credit Scores
- Fintech
- Lending
- Personal Finance
- Spectral
- Linting
- API Governance
---
