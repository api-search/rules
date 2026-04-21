---
categories:
- avaloq
description: Spectral linting rules defining API design standards and conventions for Avaloq.
layout: rules
name: Avaloq API Rules
provider_name: Avaloq
provider_slug: avaloq
rule_count: 25
rules:
- description: Avaloq APIs must have a title in the info object.
  given: $.info
  name: avaloq-info-title-required
  severity: error
- description: Avaloq APIs must define a version.
  given: $.info
  name: avaloq-info-version-required
  severity: error
- description: Avaloq APIs must have a description.
  given: $.info
  name: avaloq-info-description-required
  severity: warn
- description: Avaloq APIs must include contact information.
  given: $.info
  name: avaloq-info-contact-required
  severity: warn
- description: Avaloq APIs must define at least one server.
  given: $
  name: avaloq-servers-required
  severity: error
- description: Avaloq server URLs must use HTTPS.
  given: $.servers[*]
  name: avaloq-server-url-https
  severity: error
- description: Avaloq path segments must use kebab-case.
  given: $.paths
  name: avaloq-paths-kebab-case
  severity: warn
- description: All Avaloq operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: avaloq-operation-summary-required
  severity: error
- description: All Avaloq operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: avaloq-operation-description-required
  severity: warn
- description: All Avaloq operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: avaloq-operation-id-required
  severity: error
- description: All Avaloq operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: avaloq-operation-tags-required
  severity: warn
- description: All Avaloq parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: avaloq-parameters-description-required
  severity: warn
- description: Avaloq request bodies must have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: avaloq-request-body-description
  severity: warn
- description: Avaloq GET operations must have a 200 response.
  given: $.paths[*].get.responses
  name: avaloq-response-200-required
  severity: error
- description: Avaloq operations must document 400 errors.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: avaloq-response-400-required
  severity: warn
- description: Avaloq operations must document 401 unauthorized.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: avaloq-response-401-required
  severity: warn
- description: Avaloq schema properties must have descriptions.
  given: $.components.schemas[*].properties[*]
  name: avaloq-schema-properties-described
  severity: warn
- description: Avaloq schema properties must have a type.
  given: $.components.schemas[*].properties[*]
  name: avaloq-schema-type-required
  severity: warn
- description: Avaloq APIs must define security schemes.
  given: $.components
  name: avaloq-security-defined
  severity: error
- description: Avaloq APIs must use Bearer/JWT authentication.
  given: $.components.securitySchemes[*]
  name: avaloq-bearer-auth-required
  severity: warn
- description: Avaloq GET operations must not have a request body.
  given: $.paths[*].get
  name: avaloq-get-no-request-body
  severity: error
- description: Avaloq DELETE operations must not have a request body.
  given: $.paths[*].delete
  name: avaloq-delete-no-request-body
  severity: warn
- description: Avaloq POST creation operations should return 201.
  given: $.paths[*].post.responses
  name: avaloq-post-returns-201
  severity: warn
- description: Avaloq schemas should have examples.
  given: $.components.schemas[*]
  name: avaloq-schema-example-provided
  severity: info
- description: Avaloq API responses must specify content type.
  given: $.paths[*][get,post,put,patch].responses[*]
  name: avaloq-response-content-type
  severity: warn
rules_file: rules/avaloq-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/avaloq/refs/heads/main/rules/avaloq-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 1
  warn: 15
slug: avaloq-spectral-rules
tags:
- Banking
- Digital Banking
- Financial Services
- Fintech
- Payments
- Wealth Management
- Spectral
- Linting
- API Governance
---
