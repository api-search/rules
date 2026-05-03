---
api_specs:
- filename: sap-sd-sales-order-openapi.yml
  format: yaml
  label: Sales Order API
  slug: sales-order
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-sales-order-openapi.yml
- filename: sap-sd-customer-master-data-openapi.yml
  format: yaml
  label: Customer Master Data API
  slug: customer-master-data
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-customer-master-data-openapi.yml
- filename: sap-sd-outbound-delivery-openapi.yml
  format: yaml
  label: Outbound Delivery API
  slug: outbound-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-outbound-delivery-openapi.yml
- filename: sap-sd-billing-document-openapi.yml
  format: yaml
  label: Billing Document API
  slug: billing-document
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-billing-document-openapi.yml
- filename: sap-sd-pricing-openapi.yml
  format: yaml
  label: Pricing API
  slug: pricing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-pricing-openapi.yml
- filename: sap-sd-sales-quotation-openapi.yml
  format: yaml
  label: Sales Quotation API
  slug: sales-quotation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-sales-quotation-openapi.yml
- filename: sap-sd-credit-management-openapi.yml
  format: yaml
  label: Credit Management API
  slug: credit-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-credit-management-openapi.yml
- filename: sap-sd-material-master-openapi.yml
  format: yaml
  label: Material Master API
  slug: material-master
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-material-master-openapi.yml
- filename: sap-sd-credit-memo-request-openapi.yml
  format: yaml
  label: Credit Memo Request API
  slug: credit-memo-request
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-credit-memo-request-openapi.yml
- filename: sap-sd-debit-memo-request-openapi.yml
  format: yaml
  label: Debit Memo Request API
  slug: debit-memo-request
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-debit-memo-request-openapi.yml
- filename: sap-sd-sales-contract-openapi.yml
  format: yaml
  label: Sales Contract API
  slug: sales-contract
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-sales-contract-openapi.yml
- filename: sap-sd-sales-inquiry-openapi.yml
  format: yaml
  label: Sales Inquiry API
  slug: sales-inquiry
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-sales-inquiry-openapi.yml
- filename: sap-sd-sales-scheduling-agreement-openapi.yml
  format: yaml
  label: Sales Scheduling Agreement API
  slug: sales-scheduling-agreement
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-sales-scheduling-agreement-openapi.yml
- filename: sap-sd-customer-return-openapi.yml
  format: yaml
  label: Customer Return API
  slug: customer-return
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-customer-return-openapi.yml
- filename: sap-sd-customer-returns-delivery-openapi.yml
  format: yaml
  label: Customer Returns Delivery API
  slug: customer-returns-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-customer-returns-delivery-openapi.yml
- filename: sap-sd-customer-material-openapi.yml
  format: yaml
  label: Customer Material API
  slug: customer-material
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-customer-material-openapi.yml
- filename: sap-sd-inbound-delivery-openapi.yml
  format: yaml
  label: Inbound Delivery API
  slug: inbound-delivery
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/openapi/sap-sd-inbound-delivery-openapi.yml
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP Sales and Distribution (SD).
layout: rules
name: SAP Sales and Distribution (SD) API Rules
provider_name: SAP Sales and Distribution (SD)
provider_slug: sap-sales-and-distribution-sd
rule_count: 17
rules:
- description: SAP OData entity set paths should use PascalCase entity names (A_EntityName pattern)
  given: $.paths[*]~
  name: sap-sd-path-odata-entity-set
  severity: warn
- description: OperationIds should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sap-sd-operation-id-camel-case
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-sd-has-tags
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-sd-has-operation-id
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-sd-has-summary
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: sap-sd-summary-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: sap-sd-has-description
  severity: warn
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: sap-sd-get-response-200
  severity: error
- description: POST create operations should have a 201 or 200 response
  given: $.paths[*].post
  name: sap-sd-post-response-201
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: sap-sd-delete-response-204
  severity: warn
- description: SAP OData collection endpoints should support $top and $skip for pagination
  given: $.paths[?(!@property.match(/\{/))].get.parameters[*].name
  name: sap-sd-odata-top-skip-params
  severity: warn
- description: API info must include contact information
  given: $.info
  name: sap-sd-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: sap-sd-info-license
  severity: warn
- description: API must define at least one server
  given: $
  name: sap-sd-servers-defined
  severity: error
- description: API must define security requirements
  given: $
  name: sap-sd-security-defined
  severity: error
- description: Schema component names should use PascalCase
  given: $.components.schemas[*]~
  name: sap-sd-components-schemas-named
  severity: warn
- description: Path items must define at least one operation
  given: $.paths[*]
  name: sap-sd-no-empty-paths
  severity: error
rules_file: rules/sap-sd-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/rules/sap-sd-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 9
slug: sap-sd-rules
source_filename: sap-sd-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n\n  # SAP OData Naming Conventions\n  sap-sd-path-odata-entity-set:\n    description: SAP OData entity set paths should use PascalCase entity names (A_EntityName pattern)\n    message: \"{{description}} - {{path}} should follow SAP OData entity set naming (e.g. A_SalesOrder)\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[A-Z][A-Za-z_]+(\\\\/|\\\\{|$)\"\n\n  sap-sd-operation-id-camel-case:\n    description: OperationIds should use camelCase\n    message: \"{{description}} - '{{value}}' should be camelCase\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sap-sd-has-tags:\n    description: All operations must have at least one tag\n    message: \"{{description}} - operation at {{path}} must include tags\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  sap-sd-has-operation-id:\n    description: All operations must have an operationId\n    message: \"{{description}} - operation at {{path}} must have operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sap-sd-has-summary:\n    description: All operations must have a summary\n    message: \"{{description}} - operation at {{path}} must have summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  sap-sd-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"{{description}} - '{{value}}' should start with an uppercase letter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-sd-has-description:\n    description: All operations should have a description\n    message: \"{{description}} - operation at {{path}} should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  sap-sd-get-response-200:\n    description: GET operations must have a 200 response\n    message: \"{{description}} - GET operation at {{path}} must define a 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  sap-sd-post-response-201:\n    description: POST create operations should have a 201 or 200 response\n    message: \"{{description}} - POST operation at {{path}} should define a 200 or 201 response\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  sap-sd-delete-response-204:\n    description: DELETE operations should return 204 No Content\n    message: \"{{description}} - DELETE operation at {{path}} should return 204\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: truthy\n\n  sap-sd-odata-top-skip-params:\n    description: SAP OData collection endpoints should support $top and $skip for pagination\n    message: \"{{description}} - Collection GET at {{path}} should support OData $top and $skip parameters\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/\\\\{/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - \"$top\"\n          - \"$skip\"\n          - \"$filter\"\n          - \"$select\"\n          - \"$expand\"\n          - \"$orderby\"\n        \
  \  - \"$inlinecount\"\n          - \"$count\"\n          - \"$format\"\n\n  sap-sd-info-contact:\n    description: API info must include contact information\n    message: \"{{description}} - info.contact is required\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sap-sd-info-license:\n    description: API info must include license information\n    message: \"{{description}} - info.license is required\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  sap-sd-servers-defined:\n    description: API must define at least one server\n    message: \"{{description}} - servers array is required and must not be empty\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  sap-sd-security-defined:\n    description: API must define security requirements\n    message: \"{{description}} - global security must be defined\"\n    severity: error\n\
  \    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  sap-sd-components-schemas-named:\n    description: Schema component names should use PascalCase\n    message: \"{{description}} - schema '{{property}}' should use PascalCase\"\n    severity: warn\n    given: \"$.components.schemas[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]*$\"\n\n  sap-sd-no-empty-paths:\n    description: Path items must define at least one operation\n    message: \"{{description}} - path {{path}} must define at least one HTTP operation\"\n    severity: error\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"get\"]\n            - required: [\"post\"]\n            - required: [\"put\"]\n            - required: [\"patch\"]\n            - required: [\"delete\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-sales-and-distribution-sd/refs/heads/main/rules/sap-sd-rules.yml
tags:
- Distribution
- ERP
- OData
- S/4HANA
- Sales
- SAP
- Spectral
- Linting
- API Governance
---
