---
api_specs:
- filename: openapi.json
  format: json
  label: TIBCO Cloud Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://integration.cloud.tibco.com/docs/api/openapi.json
- filename: io-docs
  format: yaml
  label: TIBCO Mashery API Management
  slug: ''
  spec_type: OpenAPI
  url: https://developer.mashery.com/io-docs
- filename: tibco-businessevents-openapi.yml
  format: yaml
  label: TIBCO BusinessEvents API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/openapi/tibco-businessevents-openapi.yml
- filename: tibco-messaging-asyncapi.yml
  format: yaml
  label: TIBCO Messaging API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/asyncapi/tibco-messaging-asyncapi.yml
- filename: tibco-spotfire-openapi.yml
  format: yaml
  label: TIBCO Spotfire Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/openapi/tibco-spotfire-openapi.yml
categories:
- tibco
description: Spectral linting rules defining API design standards and conventions for TIBCO.
layout: rules
name: TIBCO API Rules
provider_name: TIBCO
provider_slug: tibco
rule_count: 13
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: tibco-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: tibco-tags-title-case
  severity: warn
- description: Path segments must use kebab-case or camelCase only
  given: $.paths[*]~
  name: tibco-paths-kebab-case
  severity: warn
- description: All operations must have security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: tibco-security-defined
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: tibco-responses-200-on-get
  severity: warn
- description: Protected operations should document 401 response
  given: $.paths[*][get,post,put,delete]
  name: tibco-responses-401-defined
  severity: info
- description: POST/PUT request bodies must define a JSON schema
  given: $.paths[*][post,put].requestBody.content.application/json
  name: tibco-request-body-json-schema
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: tibco-servers-https-only
  severity: error
- description: API info must specify a version
  given: $.info
  name: tibco-info-version-defined
  severity: error
- description: API info must include contact information
  given: $.info
  name: tibco-info-contact-defined
  severity: warn
- description: Response schemas should use $ref to component schemas
  given: $.paths[*][*].responses.200.content[*].schema
  name: tibco-component-schemas-use-refs
  severity: info
- description: Resource identifier path parameters should end with 'Id'
  given: $.paths[*][*].parameters[?(@.in == 'path')].name
  name: tibco-ids-in-path-params
  severity: info
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: tibco-delete-returns-204
  severity: info
rules_file: rules/tibco-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/rules/tibco-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 4
  warn: 5
slug: tibco-rules
source_filename: tibco-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  tibco-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  tibco-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]+$\"\n\n  tibco-paths-kebab-case:\n    description: Path segments must use kebab-case or camelCase only\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z][a-zA-Z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]+\\\\})*$\"\n\n  tibco-security-defined:\n    description: All operations must have security requirements\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n     \
  \ field: security\n      function: defined\n\n  tibco-responses-200-on-get:\n    description: GET operations must have a 200 response\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  tibco-responses-401-defined:\n    description: Protected operations should document 401 response\n    severity: info\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: responses.401\n      function: defined\n\n  tibco-request-body-json-schema:\n    description: POST/PUT request bodies must define a JSON schema\n    severity: error\n    given: \"$.paths[*][post,put].requestBody.content.application/json\"\n    then:\n      field: schema\n      function: defined\n\n  tibco-servers-https-only:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  tibco-info-version-defined:\n \
  \   description: API info must specify a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: defined\n\n  tibco-info-contact-defined:\n    description: API info must include contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  tibco-component-schemas-use-refs:\n    description: Response schemas should use $ref to component schemas\n    severity: info\n    given: \"$.paths[*][*].responses.200.content[*].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"$ref\"]\n            - required: [\"type\"]\n\n  tibco-ids-in-path-params:\n    description: Resource identifier path parameters should end with 'Id'\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^.*[Ii]d$\"\n\n  tibco-delete-returns-204:\n\
  \    description: DELETE operations should return 204 No Content\n    severity: info\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tibco/refs/heads/main/rules/tibco-rules.yml
tags:
- Analytics
- API Management
- Cloud
- Enterprise Software
- Integration
- Messaging
- Real-Time Data
- Spectral
- Linting
- API Governance
---
