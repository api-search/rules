---
api_specs:
- filename: resources_list.htm
  format: yaml
  label: Salesforce Service Cloud REST API
  slug: ''
  spec_type: OpenAPI
  url: https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_list.htm
- filename: salesforce-streaming-api-asyncapi.yml
  format: yaml
  label: Service Cloud Streaming API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/asyncapi/salesforce-streaming-api-asyncapi.yml
- filename: salesforce-live-agent-openapi.yml
  format: yaml
  label: Live Agent REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/openapi/salesforce-live-agent-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Service Cloud.
layout: rules
name: Salesforce Service Cloud API Rules
provider_name: Salesforce Service Cloud
provider_slug: salesforce-service-cloud
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesforce-svc-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: salesforce-svc-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: salesforce-svc-tags-title-case
  severity: warn
- description: All 200 responses must have a description
  given: $.paths[*][*].responses['200']
  name: salesforce-svc-response-200-description
  severity: error
- description: API info must include contact details
  given: $.info
  name: salesforce-svc-contact-required
  severity: error
- description: API info must include a version
  given: $.info
  name: salesforce-svc-version-required
  severity: error
- description: API must define at least one server
  given: $
  name: salesforce-svc-servers-required
  severity: error
- description: API must define security requirements
  given: $
  name: salesforce-svc-security-defined
  severity: error
- description: Case status values should be documented in schema
  given: $.components.schemas.Case.properties.Status
  name: salesforce-svc-case-status-documented
  severity: warn
- description: Case ID path parameters should be defined in components
  given: $.components.parameters
  name: salesforce-svc-case-id-parameter-defined
  severity: info
rules_file: rules/salesforce-service-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/rules/salesforce-service-cloud-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 4
slug: salesforce-service-cloud-rules
source_filename: salesforce-service-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  salesforce-svc-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-svc-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  salesforce-svc-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-svc-response-200-description:\n    description: All 200 responses must have a description\n    severity: error\n\
  \    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: description\n      function: truthy\n\n  salesforce-svc-contact-required:\n    description: API info must include contact details\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salesforce-svc-version-required:\n    description: API info must include a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  salesforce-svc-servers-required:\n    description: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  salesforce-svc-security-defined:\n    description: API must define security requirements\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  salesforce-svc-case-status-documented:\n    description: Case status values should be documented in schema\n    message: \"\
  Case Status field should define enum values\"\n    severity: warn\n    given: \"$.components.schemas.Case.properties.Status\"\n    then:\n      function: truthy\n\n  salesforce-svc-case-id-parameter-defined:\n    description: Case ID path parameters should be defined in components\n    severity: info\n    given: \"$.components.parameters\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-service-cloud/refs/heads/main/rules/salesforce-service-cloud-rules.yml
tags:
- Case Management
- CRM
- Customer Service
- Help Desk
- Support
- Ticketing
- Spectral
- Linting
- API Governance
---
