---
api_specs:
- filename: scrapfly-scrape-openapi.yml
  format: yaml
  label: Scrapfly Scrape API
  slug: scrape-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scrapfly/refs/heads/main/openapi/scrapfly-scrape-openapi.yml
categories:
- scrapfly
description: Spectral linting rules defining API design standards and conventions for Scrapfly.
layout: rules
name: Scrapfly API Rules
provider_name: Scrapfly
provider_slug: scrapfly
rule_count: 9
rules:
- description: All operations must include the API key query parameter
  given: $.paths[*][get,post].parameters
  name: scrapfly-api-key-query-param
  severity: error
- description: Scrape endpoints must include the 'url' parameter
  given: $.paths['/scrape'][get,post].parameters
  name: scrapfly-url-param-required
  severity: error
- description: All operations must have operationId
  given: $.paths[*][*]
  name: scrapfly-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: scrapfly-tags-required
  severity: warn
- description: Scrape responses should document credit consumption headers
  given: $.paths['/scrape'].get.responses['200']
  name: scrapfly-response-credit-headers
  severity: info
- description: Boolean parameters should have explicit default values
  given: $.paths[*][*].parameters[?(@.schema.type === 'boolean')]
  name: scrapfly-boolean-default-values
  severity: warn
- description: Operations should document error responses
  given: $.paths[*][*].responses
  name: scrapfly-error-responses
  severity: warn
- description: Parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: scrapfly-parameter-descriptions
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: scrapfly-camel-case-operation-ids
  severity: warn
rules_file: rules/scrapfly-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scrapfly/refs/heads/main/rules/scrapfly-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: scrapfly-rules
source_filename: scrapfly-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  scrapfly-api-key-query-param:\n    description: All operations must include the API key query parameter\n    message: \"Scrapfly operations must include 'key' query parameter for authentication\"\n    severity: error\n    given: \"$.paths[*][get,post].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                const: key\n              in:\n                const: query\n\n  scrapfly-url-param-required:\n    description: Scrape endpoints must include the 'url' parameter\n    message: \"Scraping operations must require the 'url' query parameter\"\n    severity: error\n    given: \"$.paths['/scrape'][get,post].parameters\"\n    then:\n      function: truthy\n\n  scrapfly-operation-ids:\n    description: All operations must have operationId\n    message: \"Every operation must have\
  \ a unique operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  scrapfly-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operations must be tagged for categorization\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  scrapfly-response-credit-headers:\n    description: Scrape responses should document credit consumption headers\n    message: \"Scrape responses should document X-Scrapfly-Api-Cost and related headers\"\n    severity: info\n    given: \"$.paths['/scrape'].get.responses['200']\"\n    then:\n      field: headers\n      function: truthy\n\n  scrapfly-boolean-default-values:\n    description: Boolean parameters should have explicit default values\n    message: \"Boolean parameters like render_js and asp should have explicit default values\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.schema.type\
  \ === 'boolean')]\"\n    then:\n      field: schema.default\n      function: defined\n\n  scrapfly-error-responses:\n    description: Operations should document error responses\n    message: \"Operations should document at least 401 and 429 error responses\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - '401'\n\n  scrapfly-parameter-descriptions:\n    description: Parameters should have descriptions\n    message: \"Parameter '{{value}}' should have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  scrapfly-camel-case-operation-ids:\n    description: Operation IDs should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase naming\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scrapfly/refs/heads/main/rules/scrapfly-rules.yml
tags:
- AI
- Data Extraction
- Screenshots
- Web Scraping
- Proxies
- Browser Automation
- Spectral
- Linting
- API Governance
---
