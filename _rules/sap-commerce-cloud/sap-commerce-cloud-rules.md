---
api_specs:
- filename: overview
  format: yaml
  label: Commerce Web Services API
  slug: ''
  spec_type: OpenAPI
  url: https://api.sap.com/api/commerce_web_services/overview
- filename: sap-commerce-cloud-assisted-service-openapi.yml
  format: yaml
  label: Assisted Service Module API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/openapi/sap-commerce-cloud-assisted-service-openapi.yml
- filename: sap-commerce-cloud-integration-openapi.yml
  format: yaml
  label: Integration API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/openapi/sap-commerce-cloud-integration-openapi.yml
- filename: sap-commerce-cloud-admin-openapi.yml
  format: yaml
  label: Admin API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/openapi/sap-commerce-cloud-admin-openapi.yml
- filename: sap-commerce-cloud-product-content-management-openapi.yml
  format: yaml
  label: Product Content Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/openapi/sap-commerce-cloud-product-content-management-openapi.yml
categories:
- sap
description: Spectral linting rules defining API design standards and conventions for SAP Commerce Cloud.
layout: rules
name: SAP Commerce Cloud API Rules
provider_name: SAP Commerce Cloud
provider_slug: sap-commerce-cloud
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sap-commerce-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: sap-commerce-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: sap-commerce-tags-title-case
  severity: warn
- description: Commerce Cloud APIs require OAuth 2.0 authentication
  given: $.components.securitySchemes
  name: sap-commerce-oauth2-required
  severity: warn
- description: GET operations should define a response schema
  given: $.paths[*].get.responses.200.content
  name: sap-commerce-response-200-schema
  severity: warn
- description: Commerce Cloud APIs support a fields parameter for response shaping
  given: $.paths[*].get.parameters
  name: sap-commerce-fields-parameter
  severity: info
- description: Collection endpoints should support currentPage and pageSize
  given: $.paths[*].get.parameters
  name: sap-commerce-pagination-parameters
  severity: info
- description: Commerce Cloud server URLs must include tenant, region, and baseSiteId variables
  given: $.servers[*].variables
  name: sap-commerce-servers-with-variables
  severity: warn
- description: Commerce APIs should support both B2B and B2C scenarios
  given: $.info.description
  name: sap-commerce-b2b-b2c-support
  severity: info
- description: Commerce APIs should use OCC v2 versioning
  given: $.servers[*].url
  name: sap-commerce-occ-versioning
  severity: info
rules_file: rules/sap-commerce-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/rules/sap-commerce-cloud-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 4
  warn: 6
slug: sap-commerce-cloud-rules
source_filename: sap-commerce-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sap-commerce-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" should be in Title Case\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-commerce-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: OperationId \"{{value}}\" should use camelCase\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sap-commerce-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    given: \"$.tags[*].name\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sap-commerce-oauth2-required:\n    description: Commerce\
  \ Cloud APIs require OAuth 2.0 authentication\n    message: APIs should specify OAuth 2.0 security\n    given: \"$.components.securitySchemes\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-commerce-response-200-schema:\n    description: GET operations should define a response schema\n    message: GET operations should return typed schemas\n    given: \"$.paths[*].get.responses.200.content\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-commerce-fields-parameter:\n    description: Commerce Cloud APIs support a fields parameter for response shaping\n    message: List/Get operations should support the 'fields' query parameter\n    given: \"$.paths[*].get.parameters\"\n    severity: info\n    then:\n      function: truthy\n\n  sap-commerce-pagination-parameters:\n    description: Collection endpoints should support currentPage and pageSize\n    message: Paginated list operations should define currentPage and pageSize parameters\n    given: \"$.paths[*].get.parameters\"\
  \n    severity: info\n    then:\n      function: truthy\n\n  sap-commerce-servers-with-variables:\n    description: Commerce Cloud server URLs must include tenant, region, and baseSiteId variables\n    message: Server URL should use variable substitution for tenant, region, and baseSiteId\n    given: \"$.servers[*].variables\"\n    severity: warn\n    then:\n      function: truthy\n\n  sap-commerce-b2b-b2c-support:\n    description: Commerce APIs should support both B2B and B2C scenarios\n    message: API description should mention B2B and B2C commerce support\n    given: \"$.info.description\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(B2B|B2C|commerce)\"\n\n  sap-commerce-occ-versioning:\n    description: Commerce APIs should use OCC v2 versioning\n    message: Commerce Web Services should reference OCC v2 in server URL\n    given: \"$.servers[*].url\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"/occ/v2\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sap-commerce-cloud/refs/heads/main/rules/sap-commerce-cloud-rules.yml
tags:
- B2B
- B2C
- Commerce
- Customer Experience
- Ecommerce
- Omnichannel
- Retail
- Spectral
- Linting
- API Governance
---
