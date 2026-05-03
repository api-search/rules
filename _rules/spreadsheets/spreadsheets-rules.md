---
api_specs:
- filename: google-sheets-openapi.yml
  format: yaml
  label: Google Sheets API
  slug: google-sheets-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spreadsheets/refs/heads/main/openapi/google-sheets-openapi.yml
categories:
- spreadsheets
description: Spectral linting rules defining API design standards and conventions for Spreadsheets.
layout: rules
name: Spreadsheets API Rules
provider_name: Spreadsheets
provider_slug: spreadsheets
rule_count: 13
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-operation-ids-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: spreadsheets-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-tags-required
  severity: error
- description: API must use OAuth 2.0 security scheme
  given: $.components.securitySchemes.OAuth2
  name: spreadsheets-oauth2-security
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: spreadsheets-response-200-get
  severity: error
- description: All operations must document 401 Unauthorized
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-response-401-required
  severity: warn
- description: All operations must document 403 Forbidden (insufficient permissions)
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-response-403-required
  severity: warn
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: spreadsheets-parameters-have-descriptions
  severity: warn
- description: Request bodies must specify application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: spreadsheets-request-body-json
  severity: error
- description: Success responses must include a schema
  given: $.paths[*].get.responses['200'].content.application/json
  name: spreadsheets-response-schema-required
  severity: warn
- description: Operations accessing spreadsheets must use spreadsheetId path parameter
  given: $.paths['/spreadsheets/{spreadsheetId}'][*].parameters[?(@.name == 'spreadsheetId')]
  name: spreadsheets-spreadsheet-id-path-param
  severity: info
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: spreadsheets-descriptions-required
  severity: warn
rules_file: rules/spreadsheets-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spreadsheets/refs/heads/main/rules/spreadsheets-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 6
slug: spreadsheets-rules
source_filename: spreadsheets-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spreadsheets-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spreadsheets-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  spreadsheets-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  spreadsheets-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  spreadsheets-oauth2-security:\n    description: API must use OAuth 2.0 security scheme\n    severity: error\n    given: \"$.components.securitySchemes.OAuth2\"\n    then:\n      function: truthy\n\n  spreadsheets-response-200-get:\n    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  spreadsheets-response-401-required:\n    description: All operations must document 401 Unauthorized\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  spreadsheets-response-403-required:\n    description: All operations must document 403 Forbidden (insufficient permissions)\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.403\n      function: truthy\n\n  spreadsheets-parameters-have-descriptions:\n    description: Parameters\
  \ must have descriptions\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spreadsheets-request-body-json:\n    description: Request bodies must specify application/json content type\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  spreadsheets-response-schema-required:\n    description: Success responses must include a schema\n    severity: warn\n    given: \"$.paths[*].get.responses['200'].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  spreadsheets-spreadsheet-id-path-param:\n    description: Operations accessing spreadsheets must use spreadsheetId path parameter\n    severity: info\n    given: \"$.paths['/spreadsheets/{spreadsheetId}'][*].parameters[?(@.name == 'spreadsheetId')]\"\n    then:\n      function: truthy\n\n  spreadsheets-descriptions-required:\n\
  \    description: Operations should have descriptions\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spreadsheets/refs/heads/main/rules/spreadsheets-rules.yml
tags:
- Spreadsheets
- Data
- Google Sheets
- Excel
- Productivity
- Automation
- Spectral
- Linting
- API Governance
---
