---
categories:
- block
description: Spectral linting rules defining API design standards and conventions for Block.
layout: rules
name: Block API Rules
provider_name: Block
provider_slug: block
rule_count: 29
rules:
- description: API must have a title
  given: $.info
  name: block-info-title
  severity: error
- description: API must have a description
  given: $.info
  name: block-info-description
  severity: error
- description: API must have a version
  given: $.info
  name: block-info-version
  severity: error
- description: API must have contact information
  given: $.info
  name: block-info-contact
  severity: warn
- description: API must have at least one server defined
  given: $
  name: block-servers-exist
  severity: error
- description: Production server must use HTTPS
  given: $.servers[*]
  name: block-server-https
  severity: error
- description: Each server must have a description
  given: $.servers[*]
  name: block-server-description
  severity: warn
- description: Path segments must use kebab-case or snake_case
  given: $.paths[*]~
  name: block-path-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: block-path-no-trailing-slash
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-id-exists
  severity: error
- description: OperationId must use kebab-case
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-id-kebab-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-summary-exists
  severity: error
- description: Operation summary must use title case and start with Block Square
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-summary-title-case
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-description-exists
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options,trace]
  name: block-operation-tags
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: block-parameter-description
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][*].parameters[*]
  name: block-parameter-schema
  severity: error
- description: Request bodies should have a description
  given: $.paths[*][*].requestBody
  name: block-request-body-description
  severity: warn
- description: Operations must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: block-response-success-exists
  severity: error
- description: Success responses must have a content schema
  given: $.paths[*][*].responses[200,201].content[*]
  name: block-response-schema-exists
  severity: warn
- description: Responses should include examples
  given: $.paths[*][*].responses[200,201].content[*]
  name: block-response-examples
  severity: warn
- description: API must define security schemes
  given: $.components
  name: block-security-scheme-defined
  severity: error
- description: API should have global security defined
  given: $
  name: block-global-security
  severity: warn
- description: All schema objects must have a type
  given: $.components.schemas[*]
  name: block-schema-type
  severity: warn
- description: All schema components must have a description
  given: $.components.schemas[*]
  name: block-schema-description
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: block-property-description
  severity: info
- description: POST operations creating resources should require idempotency_key
  given: $.paths[*].post.requestBody.content[*].schema.required[*]
  name: block-idempotency-key
  severity: warn
- description: Money amounts should use the Money object pattern with amount and currency
  given: $.components.schemas[*].properties[*_money]
  name: block-money-object
  severity: info
- description: List operations should support cursor-based pagination
  given: $.paths[*].get.parameters[*]
  name: block-cursor-pagination
  severity: info
rules_file: rules/block-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/block/refs/heads/main/rules/block-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 3
  warn: 15
slug: block-spectral-rules
tags:
- Commerce
- Cryptocurrency
- eCommerce
- Fintech
- Payments
- Point Of Sale
- Square
- Spectral
- Linting
- API Governance
---
