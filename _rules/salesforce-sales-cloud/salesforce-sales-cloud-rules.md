---
api_specs:
- filename: salesforce-sales-cloud-rest-api-openapi.yml
  format: yaml
  label: Salesforce REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-rest-api-openapi.yml
- filename: salesforce-sales-cloud-bulk-api-openapi.yml
  format: yaml
  label: Bulk API 2.0
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-bulk-api-openapi.yml
- filename: salesforce-sales-cloud-platform-events-api-openapi.yml
  format: yaml
  label: Platform Events API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-platform-events-api-openapi.yml
- filename: salesforce-sales-cloud-analytics-api-openapi.yml
  format: yaml
  label: Analytics REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-analytics-api-openapi.yml
- filename: salesforce-sales-cloud-composite-api-openapi.yml
  format: yaml
  label: Salesforce Composite API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-composite-api-openapi.yml
- filename: salesforce-sales-cloud-graphql-api-openapi.yml
  format: yaml
  label: Salesforce GraphQL API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-graphql-api-openapi.yml
- filename: salesforce-sales-cloud-tooling-api-openapi.yml
  format: yaml
  label: Salesforce Tooling API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-tooling-api-openapi.yml
- filename: salesforce-sales-cloud-change-data-capture-api-openapi.yml
  format: yaml
  label: Salesforce Change Data Capture API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-change-data-capture-api-openapi.yml
- filename: salesforce-sales-cloud-connect-api-openapi.yml
  format: yaml
  label: Salesforce Connect REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-connect-api-openapi.yml
- filename: salesforce-sales-cloud-ui-api-openapi.yml
  format: yaml
  label: Salesforce User Interface API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-ui-api-openapi.yml
- filename: salesforce-sales-cloud-apex-rest-api-openapi.yml
  format: yaml
  label: Salesforce Apex REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/openapi/salesforce-sales-cloud-apex-rest-api-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Sales Cloud.
layout: rules
name: Salesforce Sales Cloud API Rules
provider_name: Salesforce Sales Cloud
provider_slug: salesforce-sales-cloud
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesforce-sc-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: salesforce-sc-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: salesforce-sc-tags-title-case
  severity: warn
- description: All 200 responses must have a description
  given: $.paths[*][*].responses['200']
  name: salesforce-sc-response-200-description
  severity: error
- description: API info must include contact details
  given: $.info
  name: salesforce-sc-contact-required
  severity: error
- description: API info must include a version
  given: $.info
  name: salesforce-sc-version-required
  severity: error
- description: API must define at least one server
  given: $
  name: salesforce-sc-servers-required
  severity: error
- description: API must define security requirements
  given: $
  name: salesforce-sc-security-defined
  severity: error
- description: sObject paths should use standard Salesforce casing conventions
  given: $.paths[*]~
  name: salesforce-sc-sobject-paths-lowercase
  severity: info
- description: Bulk API job creation should accept application/json
  given: $.paths./jobs/ingest.post.requestBody.content
  name: salesforce-sc-bulk-job-content-type
  severity: warn
rules_file: rules/salesforce-sales-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/rules/salesforce-sales-cloud-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 4
slug: salesforce-sales-cloud-rules
source_filename: salesforce-sales-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  salesforce-sc-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-sc-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  salesforce-sc-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-sc-response-200-description:\n    description: All 200\
  \ responses must have a description\n    severity: error\n    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: description\n      function: truthy\n\n  salesforce-sc-contact-required:\n    description: API info must include contact details\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salesforce-sc-version-required:\n    description: API info must include a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  salesforce-sc-servers-required:\n    description: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  salesforce-sc-security-defined:\n    description: API must define security requirements\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  salesforce-sc-sobject-paths-lowercase:\n    description: sObject paths\
  \ should use standard Salesforce casing conventions\n    message: \"Path '{{value}}' should follow Salesforce sObject naming conventions\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-zA-Z/{}._-]+$\"\n\n  salesforce-sc-bulk-job-content-type:\n    description: Bulk API job creation should accept application/json\n    message: \"Bulk API endpoints should accept application/json content type\"\n    severity: warn\n    given: \"$.paths./jobs/ingest.post.requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-sales-cloud/refs/heads/main/rules/salesforce-sales-cloud-rules.yml
tags:
- Cloud
- CRM
- Customer Management
- Enterprise
- Sales
- Spectral
- Linting
- API Governance
---
