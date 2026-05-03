---
api_specs:
- filename: openapi.json
  format: json
  label: RHEL 8 Subscription Management API
  slug: subscription-management-api
  spec_type: OpenAPI
  url: https://api.access.redhat.com/management/v1/openapi.json
- filename: openapi.json
  format: json
  label: RHEL 8 Insights API
  slug: insights-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/insights/v1/openapi.json
- filename: openapi.json
  format: json
  label: RHEL 8 Image Builder API
  slug: image-builder-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/image-builder/v1/openapi.json
- filename: openapi.json
  format: json
  label: RHEL 8 Patch Management API
  slug: patch-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/patch/v3/openapi.json
- filename: openapi.json
  format: json
  label: RHEL 8 Vulnerability Management API
  slug: vulnerability-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/vulnerability/v1/openapi.json
- filename: openapi.json
  format: json
  label: RHEL 8 Compliance API
  slug: compliance-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/compliance/v2/openapi.json
- filename: red-hat-enterprise-linux-8-security-data-openapi.yml
  format: yaml
  label: RHEL 8 Security Data API
  slug: security-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-enterprise-linux-8/refs/heads/main/openapi/red-hat-enterprise-linux-8-security-data-openapi.yml
- filename: openapi.json
  format: json
  label: RHEL 8 Host Inventory API
  slug: host-inventory-api
  spec_type: OpenAPI
  url: https://console.redhat.com/api/inventory/v1/openapi.json
categories:
- rhel
description: Spectral linting rules defining API design standards and conventions for Red Hat Enterprise Linux 8.
layout: rules
name: Red Hat Enterprise Linux 8 API Rules
provider_name: Red Hat Enterprise Linux 8
provider_slug: red-hat-enterprise-linux-8
rule_count: 11
rules:
- description: All RHEL API operations must have an operationId to support SDK generation, documentation generation, and tooling integration.
  given: $.paths[*][get,post,put,delete,patch]
  name: rhel-operation-id-required
  severity: error
- description: Operation summaries must use Title Case to match Red Hat documentation standards.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: rhel-summary-title-case
  severity: warn
- description: All operations must have a detailed description explaining the endpoint purpose, parameters, and expected behavior.
  given: $.paths[*][get,post,put,delete,patch]
  name: rhel-operation-description
  severity: warn
- description: All query and path parameters must have descriptions to help API consumers understand accepted values.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: rhel-parameter-description
  severity: warn
- description: All RHEL Console APIs require authentication. Security schemes must be defined in the components/securitySchemes section.
  given: $.components.securitySchemes
  name: rhel-security-defined
  severity: error
- description: All operations must define at least one 2xx response to document successful operation outcomes.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: rhel-success-response
  severity: error
- description: RHEL API responses should use application/json content type for consistent integration.
  given: $.paths[*][get,post,put,patch].responses[200,201,202].content
  name: rhel-json-response-type
  severity: warn
- description: CVE identifier parameters must follow the standard CVE-YYYY-NNNNN format for compatibility with vulnerability databases.
  given: $.paths[*][get].parameters[?(@.name === 'CVE')].schema
  name: rhel-cve-format
  severity: warn
- description: List endpoints returning collections should support pagination parameters (page, per_page) for handling large datasets.
  given: $.paths[*][get]
  name: rhel-list-pagination
  severity: info
- description: API info must include contact information with a URL pointing to Red Hat support or documentation resources.
  given: $.info
  name: rhel-contact-info
  severity: warn
- description: APIs should include externalDocs pointing to the official Red Hat documentation for comprehensive integration guidance.
  given: $
  name: rhel-external-docs
  severity: info
rules_file: rules/red-hat-enterprise-linux-8-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/red-hat-enterprise-linux-8/refs/heads/main/rules/red-hat-enterprise-linux-8-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 6
slug: red-hat-enterprise-linux-8-rules
source_filename: red-hat-enterprise-linux-8-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # RHEL API operations must have operation IDs\n  rhel-operation-id-required:\n    description: >-\n      All RHEL API operations must have an operationId to support SDK\n      generation, documentation generation, and tooling integration.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  # Operation summaries use Title Case\n  rhel-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case to match Red Hat documentation\n      standards.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ,()-]+$\"\n\n  # Operations require descriptions\n  rhel-operation-description:\n    description: >-\n      All operations must have a detailed description explaining the endpoint\n      purpose, parameters, and expected behavior.\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  # Parameters need descriptions\n  rhel-parameter-description:\n    description: >-\n      All query and path parameters must have descriptions to help API\n      consumers understand accepted values.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  # Security schemes must be defined\n  rhel-security-defined:\n    description: >-\n      All RHEL Console APIs require authentication. Security schemes must\n      be defined in the components/securitySchemes section.\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  # Responses should include success status codes\n  rhel-success-response:\n    description: >-\n      All operations must define at least one 2xx response to document\n      successful operation\
  \ outcomes.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['202']\n            - required: ['204']\n\n  # JSON content type for responses\n  rhel-json-response-type:\n    description: >-\n      RHEL API responses should use application/json content type\n      for consistent integration.\n    severity: warn\n    given: $.paths[*][get,post,put,patch].responses[200,201,202].content\n    then:\n      field: application/json\n      function: truthy\n\n  # CVE IDs should follow standard format\n  rhel-cve-format:\n    description: >-\n      CVE identifier parameters must follow the standard CVE-YYYY-NNNNN\n      format for compatibility with vulnerability databases.\n    severity: warn\n    given: $.paths[*][get].parameters[?(@.name === 'CVE')].schema\n    then:\n      field:\
  \ pattern\n      function: truthy\n\n  # Pagination for list endpoints\n  rhel-list-pagination:\n    description: >-\n      List endpoints returning collections should support pagination\n      parameters (page, per_page) for handling large datasets.\n    severity: info\n    given: $.paths[*][get]\n    then:\n      function: truthy\n\n  # Contact information required in API info\n  rhel-contact-info:\n    description: >-\n      API info must include contact information with a URL pointing to\n      Red Hat support or documentation resources.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # External docs should reference Red Hat documentation\n  rhel-external-docs:\n    description: >-\n      APIs should include externalDocs pointing to the official Red Hat\n      documentation for comprehensive integration guidance.\n    severity: info\n    given: $\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red-hat-enterprise-linux-8/refs/heads/main/rules/red-hat-enterprise-linux-8-rules.yml
tags:
- Enterprise
- Linux
- Operating System
- Red Hat
- RHEL
- Spectral
- Linting
- API Governance
---
