---
api_specs:
- filename: overview
  format: yaml
  label: SAP Convergent Charging API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/convergent_charging/overview
- filename: overview
  format: yaml
  label: SAP Convergent Invoicing API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/convergent_invoicing/overview
- filename: overview
  format: yaml
  label: SAP Subscription Billing API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/subscription_billing/overview
- filename: overview
  format: yaml
  label: SAP Contract Accounts Receivable and Payable API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/fica/overview
- filename: overview
  format: yaml
  label: SAP BRIM Usage Data Intake API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/usage_data_intake/overview
- filename: overview
  format: yaml
  label: SAP Revenue Accounting and Reporting API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/revenue_accounting/overview
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP BRIM (Billing and Revenue Innovation Management).
layout: rules
name: SAP BRIM (Billing and Revenue Innovation Management) API Rules
provider_name: SAP BRIM (Billing and Revenue Innovation Management)
provider_slug: sap-brim-billing-and-revenue-innovation-management
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sap-brim-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: sap-brim-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: sap-brim-tags-title-case
  severity: warn
- description: API paths should use kebab-case for segments
  given: $.paths
  name: sap-brim-path-kebab-case
  severity: warn
- description: BRIM APIs require OAuth 2.0 or API Key authentication
  given: $.components.securitySchemes
  name: sap-brim-oauth2-or-apikey-required
  severity: warn
- description: Operations should define error responses (400, 401, 500)
  given: $.paths[*][*].responses
  name: sap-brim-error-responses
  severity: warn
- description: Subscription status fields should use defined enum values
  given: $.components.schemas.Subscription.properties.status.enum
  name: sap-brim-subscription-status-enum
  severity: info
- description: POST and PUT operations must define request bodies
  given: $.paths[*].post.requestBody
  name: sap-brim-request-body-required
  severity: warn
- description: List operations should support offset/limit pagination
  given: $.paths[*].get.parameters
  name: sap-brim-pagination-parameters
  severity: info
- description: APIs must define production and sandbox server URLs
  given: $.servers
  name: sap-brim-servers-defined
  severity: warn
rules_file: rules/sap-brim-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-brim-billing-and-revenue-innovation-management/refs/heads/main/rules/sap-brim-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 2
  warn: 8
slug: sap-brim-rules
source_filename: sap-brim-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sap-brim-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" should be in Title Case\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-brim-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: OperationId \"{{value}}\" should use camelCase\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sap-brim-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-brim-path-kebab-case:\n    description: API paths should use\
  \ kebab-case for segments\n    message: Path should use kebab-case for all segments\n    given: \"$.paths\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)*$\"\n\n  sap-brim-oauth2-or-apikey-required:\n    description: BRIM APIs require OAuth 2.0 or API Key authentication\n    message: APIs should define OAuth2 or ApiKey security schemes\n    given: \"$.components.securitySchemes\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-brim-error-responses:\n    description: Operations should define error responses (400, 401, 500)\n    message: Operation should define standard error responses\n    given: \"$.paths[*][*].responses\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-brim-subscription-status-enum:\n    description: Subscription status fields should use defined enum values\n    message: Subscription status should be ACTIVE, SUSPENDED,\
  \ CANCELLED, EXPIRED, PENDING, or TRIAL\n    given: \"$.components.schemas.Subscription.properties.status.enum\"\n    severity: info\n    then:\n      function: truthy\n\n  sap-brim-request-body-required:\n    description: POST and PUT operations must define request bodies\n    message: POST/PUT operations should define a requestBody\n    given: \"$.paths[*].post.requestBody\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-brim-pagination-parameters:\n    description: List operations should support offset/limit pagination\n    message: Collection endpoints should define offset and limit pagination parameters\n    given: \"$.paths[*].get.parameters\"\n    severity: info\n    then:\n      function: truthy\n\n  sap-brim-servers-defined:\n    description: APIs must define production and sandbox server URLs\n    message: API should define both production and sandbox server environments\n    given: \"$.servers\"\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: array\n          minItems: 1\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-brim-billing-and-revenue-innovation-management/refs/heads/main/rules/sap-brim-rules.yml
tags:
- Billing
- Enterprise
- Order to Cash
- Revenue Management
- SAP
- Subscription Management
- Usage-Based Pricing
- Spectral
- Linting
- API Governance
---
