---
api_specs:
- filename: uscis-case-status-api-openapi.yml
  format: yaml
  label: USCIS Case Status API
  slug: uscis-case-status-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-citizenship-and-immigration-services/refs/heads/main/openapi/uscis-case-status-api-openapi.yml
- filename: uscis-foia-api-openapi.yml
  format: yaml
  label: USCIS FOIA Request and Status API
  slug: uscis-foia-request-and-status-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-citizenship-and-immigration-services/refs/heads/main/openapi/uscis-foia-api-openapi.yml
categories:
- uscis
description: Spectral linting rules defining API design standards and conventions for US Citizenship and Immigration Services.
layout: rules
name: US Citizenship and Immigration Services API Rules
provider_name: US Citizenship and Immigration Services
provider_slug: us-citizenship-and-immigration-services
rule_count: 12
rules:
- description: USCIS API specs must include contact information
  given: $.info
  name: uscis-info-contact
  severity: warn
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: uscis-operation-tags
  severity: warn
- description: All operations must have a summary in Title Case
  given: $.paths[*][get,post,put,patch,delete]
  name: uscis-operation-summary
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: uscis-operation-id
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: uscis-operation-description
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: uscis-parameter-description
  severity: warn
- description: USCIS APIs should use OAuth 2.0 security
  given: $.components.securitySchemes
  name: uscis-oauth2-security
  severity: warn
- description: All 200/201 responses must have a schema
  given: $.paths[*][get,post,put,patch,delete].responses[200,201]
  name: uscis-response-schema
  severity: warn
- description: Receipt number path parameters should have a pattern
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'receiptNumber')]
  name: uscis-receipt-number-pattern
  severity: info
- description: Operations should document 401 and 429 error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: uscis-error-responses
  severity: warn
- description: USCIS API should use JSON content types
  given: $.paths[*][post,put,patch].requestBody.content
  name: uscis-json-content-type
  severity: warn
- description: API must specify version
  given: $.info
  name: uscis-version-in-info
  severity: error
rules_file: rules/uscis-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-citizenship-and-immigration-services/refs/heads/main/rules/uscis-api-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 8
slug: uscis-api-rules
source_filename: uscis-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  uscis-info-contact:\n    description: USCIS API specs must include contact information\n    message: \"Contact information is required in info object\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  uscis-operation-tags:\n    description: All operations must be tagged\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  uscis-operation-summary:\n    description: All operations must have a summary in Title Case\n    message: \"Operation '{{property}}' must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  uscis-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: operationId\n      function: truthy\n\n  uscis-operation-description:\n    description: All operations must have a description\n    message: \"Operation must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  uscis-parameter-description:\n    description: All parameters must have a description\n    message: \"Parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  uscis-oauth2-security:\n    description: USCIS APIs should use OAuth 2.0 security\n    message: \"Security schemes should include OAuth2\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  uscis-response-schema:\n    description: All 200/201 responses must have a schema\n    message: \"Successful responses\
  \ must have content with schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200,201]\"\n    then:\n      field: content\n      function: truthy\n\n  uscis-receipt-number-pattern:\n    description: Receipt number path parameters should have a pattern\n    message: \"Receipt number parameter should have pattern validation\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'receiptNumber')]\"\n    then:\n      field: schema.pattern\n      function: truthy\n\n  uscis-error-responses:\n    description: Operations should document 401 and 429 error responses\n    message: \"Operations should document 401 Unauthorized responses\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  uscis-json-content-type:\n    description: USCIS API should use JSON content types\n    message: \"Request and response bodies must use application/json\"\
  \n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  uscis-version-in-info:\n    description: API must specify version\n    message: \"API must include version information\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-citizenship-and-immigration-services/refs/heads/main/rules/uscis-api-rules.yml
tags:
- Federal Government
- Immigration
- Citizenship
- Case Status
- FOIA
- Spectral
- Linting
- API Governance
---
