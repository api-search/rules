---
api_specs:
- filename: overview
  format: yaml
  label: SAP Analytics Cloud API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/API_ANALYTICS_CLOUD/overview
- filename: overview
  format: yaml
  label: SAP BusinessObjects BI Platform REST API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/BOBJ_BIPLATFORM/overview
- filename: sap-bi-bw4hana-odata-openapi.yml
  format: yaml
  label: SAP BW/4HANA OData API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-bi/refs/heads/main/openapi/sap-bi-bw4hana-odata-openapi.yml
- filename: overview
  format: yaml
  label: SAP Datasphere API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/datasphere/overview
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP Business Intelligence.
layout: rules
name: SAP Business Intelligence API Rules
provider_name: SAP Business Intelligence
provider_slug: sap-bi
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sap-bi-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: sap-bi-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: sap-bi-tags-title-case
  severity: warn
- description: API path segments must use kebab-case or camelCase (SAP convention)
  given: $.paths
  name: sap-bi-path-kebab-case
  severity: info
- description: SAP Business Intelligence APIs require OAuth 2.0 security
  given: $.components.securitySchemes
  name: sap-bi-oauth2-required
  severity: warn
- description: GET operations must define a 200 response schema
  given: $.paths[*].get.responses.200.content
  name: sap-bi-response-200-schema
  severity: warn
- description: API info must include contact information
  given: $.info.contact
  name: sap-bi-contact-info
  severity: warn
- description: APIs must define at least one server URL
  given: $.servers
  name: sap-bi-servers-defined
  severity: error
- description: APIs should define reusable schemas in components
  given: $.components.schemas
  name: sap-bi-components-schemas
  severity: info
- description: Collection endpoints should support pagination parameters
  given: $.paths[*].get.parameters
  name: sap-bi-pagination-params
  severity: info
rules_file: rules/sap-bi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-bi/refs/heads/main/rules/sap-bi-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 6
slug: sap-bi-rules
source_filename: sap-bi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sap-bi-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" should be in Title Case\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-bi-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: OperationId \"{{value}}\" should use camelCase\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sap-bi-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-bi-path-kebab-case:\n    description: API path segments must use kebab-case\
  \ or camelCase (SAP convention)\n    message: Path segment should use lowercase with hyphens or camelCase\n    given: \"$.paths\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z][a-zA-Z0-9-]*(/[a-zA-Z][a-zA-Z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)*$\"\n\n  sap-bi-oauth2-required:\n    description: SAP Business Intelligence APIs require OAuth 2.0 security\n    message: APIs should specify OAuth 2.0 or token-based security\n    given: \"$.components.securitySchemes\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-response-200-schema:\n    description: GET operations must define a 200 response schema\n    message: GET operation should define a 200 response with content\n    given: \"$.paths[*].get.responses.200.content\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-contact-info:\n    description: API info must include contact information\n    message: API info should include a contact\
  \ block\n    given: \"$.info.contact\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-servers-defined:\n    description: APIs must define at least one server URL\n    message: API should define at least one server in the servers array\n    given: \"$.servers\"\n    severity: error\n    then:\n      function: truthy\n\n  sap-bi-components-schemas:\n    description: APIs should define reusable schemas in components\n    message: API should define schemas in components.schemas for reusability\n    given: \"$.components.schemas\"\n    severity: info\n    then:\n      function: truthy\n\n  sap-bi-pagination-params:\n    description: Collection endpoints should support pagination parameters\n    message: List operations should define limit/offset or $top/$skip pagination parameters\n    given: \"$.paths[*].get.parameters\"\n    severity: info\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-bi/refs/heads/main/rules/sap-bi-rules.yml
tags:
- Analytics
- Business Intelligence
- Data Visualization
- Reporting
- SAP
- Spectral
- Linting
- API Governance
---
