---
api_specs:
- filename: us-bank-corporate-account-information-openapi.yml
  format: yaml
  label: US Bank Corporate Account Information API
  slug: us-bank-corporate-account-information
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/openapi/us-bank-corporate-account-information-openapi.yml
- filename: us-bank-rtp-openapi.yml
  format: yaml
  label: US Bank RTP Real-Time Payments API
  slug: us-bank-rtp
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/openapi/us-bank-rtp-openapi.yml
- filename: us-bank-ach-originations-openapi.yml
  format: yaml
  label: US Bank ACH Originations API
  slug: us-bank-ach-originations
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/openapi/us-bank-ach-originations-openapi.yml
- filename: us-bank-positive-pay-openapi.yml
  format: yaml
  label: US Bank Positive Pay API
  slug: us-bank-positive-pay
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/openapi/us-bank-positive-pay-openapi.yml
- filename: us-bank-push-to-card-openapi.yml
  format: yaml
  label: US Bank Push to Card API
  slug: us-bank-push-to-card
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/openapi/us-bank-push-to-card-openapi.yml
categories:
- usbank
description: Spectral linting rules defining API design standards and conventions for US Bancorp.
layout: rules
name: US Bancorp API Rules
provider_name: US Bancorp
provider_slug: us-bancorp
rule_count: 9
rules:
- description: All US Bank API operations must have at least one tag for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: usbank-operations-have-tags
  severity: warn
- description: All US Bank API operations must accept a Correlation-ID header for tracing
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'Correlation-ID')]
  name: usbank-correlation-id-required
  severity: warn
- description: All US Bank API servers must use HTTPS
  given: $.servers[*].url
  name: usbank-https-servers
  severity: error
- description: All operations must have operationId for SDK generation
  given: $.paths[*][get,post,put,patch,delete]
  name: usbank-operations-have-operation-ids
  severity: warn
- description: US Bank operation IDs should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: usbank-operation-ids-camel-case
  severity: info
- description: All 200/201 responses should define content schema
  given: $.paths[*][*].responses[?(@property == '200' || @property == '201')]
  name: usbank-responses-have-content
  severity: warn
- description: All POST/PUT/PATCH operations should define 400 error responses
  given: $.paths[*][post,put,patch]
  name: usbank-error-responses-defined
  severity: warn
- description: US Bank API operations should have security defined (OAuth MFA)
  given: $.security
  name: usbank-security-defined
  severity: error
- description: All parameters should include descriptions
  given: $.paths[*][*].parameters[*]
  name: usbank-parameters-have-descriptions
  severity: warn
rules_file: rules/us-bank-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/rules/us-bank-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: us-bank-rules
source_filename: us-bank-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  usbank-operations-have-tags:\n    description: All US Bank API operations must have at least one tag for grouping\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  usbank-correlation-id-required:\n    description: All US Bank API operations must accept a Correlation-ID header for tracing\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'Correlation-ID')]\"\n    then:\n      field: required\n      function: truthy\n\n  usbank-https-servers:\n    description: All US Bank API servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  usbank-operations-have-operation-ids:\n    description: All operations must have operationId for SDK generation\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: operationId\n      function: truthy\n\n  usbank-operation-ids-camel-case:\n    description: US Bank operation IDs should use camelCase\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  usbank-responses-have-content:\n    description: All 200/201 responses should define content schema\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property == '200' || @property == '201')]\"\n    then:\n      field: content\n      function: truthy\n\n  usbank-error-responses-defined:\n    description: All POST/PUT/PATCH operations should define 400 error responses\n    severity: warn\n    given: \"$.paths[*][post,put,patch]\"\n    then:\n      field: responses.400\n      function: truthy\n\n  usbank-security-defined:\n    description: US Bank API operations should have security defined (OAuth MFA)\n    severity: error\n    given:\
  \ \"$.security\"\n    then:\n      function: truthy\n\n  usbank-parameters-have-descriptions:\n    description: All parameters should include descriptions\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-bancorp/refs/heads/main/rules/us-bank-rules.yml
tags:
- Banking
- Finance
- Fortune 500
- Corporate Banking
- Payments
- Open Banking
- Treasury Management
- Consumer Banking
- Spectral
- Linting
- API Governance
---
