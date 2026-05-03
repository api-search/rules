---
api_specs:
- filename: overview
  format: yaml
  label: SAP Analytics Cloud API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/SACOpenAPI/overview
- filename: overview
  format: yaml
  label: SAP HANA Cloud Data Lake Files REST API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/HanaCloudDataLake/overview
- filename: overview
  format: yaml
  label: SAP Datasphere API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/Datasphere/overview
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP BI Tools.
layout: rules
name: SAP BI Tools API Rules
provider_name: SAP BI Tools
provider_slug: sap-bi-tools
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sap-bi-tools-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: sap-bi-tools-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: sap-bi-tools-tags-title-case
  severity: warn
- description: API path segments must use kebab-case
  given: $.paths
  name: sap-bi-tools-path-kebab-case
  severity: warn
- description: SAP Analytics Cloud APIs require OAuth 2.0 security
  given: $.components.securitySchemes
  name: sap-bi-tools-oauth2-required
  severity: warn
- description: GET operations must define a 200 response schema
  given: $.paths[*].get.responses.200.content
  name: sap-bi-tools-response-200-schema
  severity: warn
- description: API info must include contact information
  given: $.info.contact
  name: sap-bi-tools-contact-info
  severity: warn
- description: APIs should reference external documentation
  given: $.externalDocs
  name: sap-bi-tools-external-docs
  severity: info
- description: APIs must define at least one server URL
  given: $.servers
  name: sap-bi-tools-servers-defined
  severity: error
- description: OData query parameters should use $-prefixed names
  given: $.paths[*][*].parameters[*].name
  name: sap-bi-tools-odata-dollar-params
  severity: info
rules_file: rules/sap-bi-tools-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-bi-tools/refs/heads/main/rules/sap-bi-tools-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 7
slug: sap-bi-tools-rules
source_filename: sap-bi-tools-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sap-bi-tools-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" should be in Title Case\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-bi-tools-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: OperationId \"{{value}}\" should use camelCase\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sap-bi-tools-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-bi-tools-path-kebab-case:\n    description: API\
  \ path segments must use kebab-case\n    message: Path segment \"{{value}}\" should use kebab-case\n    given: \"$.paths\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)*$\"\n\n  sap-bi-tools-oauth2-required:\n    description: SAP Analytics Cloud APIs require OAuth 2.0 security\n    message: Operations should specify OAuth 2.0 security\n    given: \"$.components.securitySchemes\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-tools-response-200-schema:\n    description: GET operations must define a 200 response schema\n    message: GET operation should define a 200 response with a schema\n    given: \"$.paths[*].get.responses.200.content\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-tools-contact-info:\n    description: API info must include contact information\n    message: API info should include a contact block\n    given:\
  \ \"$.info.contact\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-bi-tools-external-docs:\n    description: APIs should reference external documentation\n    message: API should include an externalDocs block pointing to SAP Help Portal\n    given: \"$.externalDocs\"\n    severity: info\n    then:\n      function: truthy\n\n  sap-bi-tools-servers-defined:\n    description: APIs must define at least one server URL\n    message: API should define at least one server in the servers array\n    given: \"$.servers\"\n    severity: error\n    then:\n      function: truthy\n\n  sap-bi-tools-odata-dollar-params:\n    description: OData query parameters should use $-prefixed names\n    message: OData parameters should follow $filter, $top, $skip, $select, $orderby naming convention\n    given: \"$.paths[*][*].parameters[*].name\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^(filter|top|skip|select|orderby|format)$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-bi-tools/refs/heads/main/rules/sap-bi-tools-rules.yml
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
