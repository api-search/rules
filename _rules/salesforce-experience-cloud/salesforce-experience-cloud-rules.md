---
api_specs:
- filename: salesforce-experience-cloud-sites-openapi.yml
  format: yaml
  label: Experience Cloud Sites API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-sites-openapi.yml
- filename: salesforce-experience-cloud-connect-communities-openapi.yml
  format: yaml
  label: Connect REST API (Communities)
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-connect-communities-openapi.yml
- filename: salesforce-experience-cloud-cms-connect-openapi.yml
  format: yaml
  label: CMS Connect API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-cms-connect-openapi.yml
- filename: salesforce-experience-cloud-rest-api-openapi.yml
  format: yaml
  label: Salesforce REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-rest-api-openapi.yml
- filename: salesforce-experience-cloud-templates-openapi.yml
  format: yaml
  label: Experience Cloud Templates API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-templates-openapi.yml
- filename: salesforce-experience-cloud-graphql-openapi.yml
  format: yaml
  label: GraphQL API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-graphql-openapi.yml
- filename: salesforce-experience-cloud-cms-managed-content-openapi.yml
  format: yaml
  label: CMS Managed Content API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-cms-managed-content-openapi.yml
- filename: salesforce-experience-cloud-cms-delivery-openapi.yml
  format: yaml
  label: CMS Delivery API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-cms-delivery-openapi.yml
- filename: salesforce-experience-cloud-user-interface-openapi.yml
  format: yaml
  label: User Interface API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/openapi/salesforce-experience-cloud-user-interface-openapi.yml
categories:
- experience
description: Spectral linting rules defining API design standards and conventions for Salesforce Experience Cloud.
layout: rules
name: Salesforce Experience Cloud API Rules
provider_name: Salesforce Experience Cloud
provider_slug: salesforce-experience-cloud
rule_count: 9
rules:
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: experience-cloud-operation-id-required
  severity: error
- description: All operations must have a non-empty summary.
  given: $.paths[*][*]
  name: experience-cloud-summary-not-empty
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: experience-cloud-tags-required
  severity: warn
- description: All operations must define a 200 or 201 response.
  given: $.paths[*][*].responses
  name: experience-cloud-response-200-required
  severity: error
- description: All Salesforce APIs require OAuth2 authentication.
  given: $.components.securitySchemes
  name: experience-cloud-oauth2-security
  severity: error
- description: Server URL should include Salesforce API version.
  given: $.servers[*].url
  name: experience-cloud-versioned-server
  severity: warn
- description: Path segments should use lowercase or camelCase (Salesforce convention).
  given: $.paths[*]~
  name: experience-cloud-path-kebab-case
  severity: hint
- description: Operations should include descriptions.
  given: $.paths[*][*]
  name: experience-cloud-description-required
  severity: hint
- description: JSON request bodies should use application/json.
  given: $.paths[*][*].requestBody.content
  name: experience-cloud-content-type-json
  severity: warn
rules_file: rules/salesforce-experience-cloud-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/rules/salesforce-experience-cloud-rules.yml
severity_counts:
  error: 4
  hint: 2
  info: 0
  warn: 3
slug: salesforce-experience-cloud-rules
source_filename: salesforce-experience-cloud-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  experience-cloud-operation-id-required:\n    description: All operations must have an operationId.\n    message: \"Operation is missing operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  experience-cloud-summary-not-empty:\n    description: All operations must have a non-empty summary.\n    message: \"Operation must have a summary.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  experience-cloud-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  experience-cloud-response-200-required:\n    description: All operations must define a 200 or 201 response.\n    message: \"Operation must define a success response.\"\
  \n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  experience-cloud-oauth2-security:\n    description: All Salesforce APIs require OAuth2 authentication.\n    message: \"API must declare OAuth2 security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"oauth2\"]\n\n  experience-cloud-versioned-server:\n    description: Server URL should include Salesforce API version.\n    message: \"Server URL should include API version (e.g., /v59.0).\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]\"\n\n  experience-cloud-path-kebab-case:\n    description: Path segments should use lowercase or camelCase (Salesforce\
  \ convention).\n    message: \"Path segments should be lowercase.\"\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9{}/._-]*)*$\"\n\n  experience-cloud-description-required:\n    description: Operations should include descriptions.\n    message: \"Operation should have a description.\"\n    severity: hint\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  experience-cloud-content-type-json:\n    description: JSON request bodies should use application/json.\n    message: \"Request body must declare application/json.\"\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"application/json\"]\n            - required: [\"multipart/form-data\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-experience-cloud/refs/heads/main/rules/salesforce-experience-cloud-rules.yml
tags:
- CMS
- Communities
- CRM
- Customer Portal
- Digital Experience
- Experience Cloud
- Partner Portal
- Spectral
- Linting
- API Governance
---
