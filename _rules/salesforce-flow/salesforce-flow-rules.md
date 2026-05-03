---
api_specs:
- filename: salesforce-flow-rest-api-openapi.yml
  format: yaml
  label: Salesforce Flow REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-flow/refs/heads/main/openapi/salesforce-flow-rest-api-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Flow.
layout: rules
name: Salesforce Flow API Rules
provider_name: Salesforce Flow
provider_slug: salesforce-flow
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesforce-flow-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: salesforce-flow-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: salesforce-flow-tags-title-case
  severity: warn
- description: All 200 responses must have a description
  given: $.paths[*][*].responses['200']
  name: salesforce-flow-response-200-description
  severity: error
- description: Path segments must use kebab-case or standard Salesforce sObject naming
  given: $.paths[*]~
  name: salesforce-flow-path-kebab-case
  severity: info
- description: Request body schemas should document required fields
  given: $.paths[*][post,put,patch].requestBody.content['application/json'].schema
  name: salesforce-flow-required-fields-documented
  severity: warn
- description: API must have contact information
  given: $.info
  name: salesforce-flow-contact-info-required
  severity: error
- description: API must have a version
  given: $.info
  name: salesforce-flow-version-present
  severity: error
- description: API must define at least one server
  given: $
  name: salesforce-flow-servers-defined
  severity: error
- description: API must define security schemes
  given: $
  name: salesforce-flow-security-defined
  severity: error
rules_file: rules/salesforce-flow-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-flow/refs/heads/main/rules/salesforce-flow-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 4
slug: salesforce-flow-rules
source_filename: salesforce-flow-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  salesforce-flow-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][^a-z]*([A-Z][^a-z]*)*\"\n\n  salesforce-flow-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  salesforce-flow-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-flow-response-200-description:\n\
  \    description: All 200 responses must have a description\n    message: \"Response '200' must have a description\"\n    severity: error\n    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: description\n      function: truthy\n\n  salesforce-flow-path-kebab-case:\n    description: Path segments must use kebab-case or standard Salesforce sObject naming\n    message: \"Path '{{value}}' should use kebab-case for custom segments\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*({[a-zA-Z]+})?)*$\"\n\n  salesforce-flow-required-fields-documented:\n    description: Request body schemas should document required fields\n    message: \"Request body schema should specify required fields\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n        \
  \  type: object\n\n  salesforce-flow-contact-info-required:\n    description: API must have contact information\n    message: \"API info must include contact details\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salesforce-flow-version-present:\n    description: API must have a version\n    message: \"API info must include a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  salesforce-flow-servers-defined:\n    description: API must define at least one server\n    message: \"API must define servers\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  salesforce-flow-security-defined:\n    description: API must define security schemes\n    message: \"API must define security requirements\"\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-flow/refs/heads/main/rules/salesforce-flow-rules.yml
tags:
- Automation
- Business Process
- CRM
- Flow
- Process Builder
- Salesforce
- Workflow
- Spectral
- Linting
- API Governance
---
