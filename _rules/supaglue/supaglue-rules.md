---
api_specs:
- filename: supaglue-management-api-openapi.yml
  format: yaml
  label: Supaglue Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/openapi/supaglue-management-api-openapi.yml
- filename: supaglue-crm-api-openapi.yml
  format: yaml
  label: Supaglue Unified CRM API
  slug: crm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/openapi/supaglue-crm-api-openapi.yml
- filename: supaglue-engagement-api-openapi.yml
  format: yaml
  label: Supaglue Unified Engagement API
  slug: engagement-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/openapi/supaglue-engagement-api-openapi.yml
- filename: supaglue-ticketing-api-openapi.yml
  format: yaml
  label: Supaglue Unified Ticketing API
  slug: ticketing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/openapi/supaglue-ticketing-api-openapi.yml
categories:
- supaglue
description: Spectral linting rules defining API design standards and conventions for Supaglue.
layout: rules
name: Supaglue API Rules
provider_name: Supaglue
provider_slug: supaglue
rule_count: 10
rules:
- description: Supaglue APIs use x-api-key header authentication. All endpoints should define security with the ApiKeyAuth scheme.
  given: $.paths[*][get,post,put,patch,delete]
  name: supaglue-apikey-header-security
  severity: warn
- description: Supaglue CRM, Engagement, and Ticketing API operations require a x-customer-id header to identify the customer context. Operations accessing customer data should document this parameter.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: supaglue-customer-id-header
  severity: info
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: supaglue-summaries-title-case
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: supaglue-operation-ids-camel-case
  severity: warn
- description: Supaglue CRM and Engagement APIs require x-provider-name header to route requests to the correct provider (e.g. salesforce, hubspot). Should be documented in operation parameters.
  given: $.paths[*][get,post,put,patch,delete].parameters
  name: supaglue-provider-name-header
  severity: info
- description: Upsert operations use /_upsert subpath convention (e.g. /contacts/_upsert, /accounts/_upsert). These should use POST method.
  given: $.paths[*~/_upsert].post
  name: supaglue-upsert-paths
  severity: info
- description: Search operations use /_search subpath convention (e.g. /contacts/_search). These should use POST method with a request body.
  given: $.paths[*~/_search].post
  name: supaglue-search-paths
  severity: info
- description: APIs must define contact information
  given: $.info
  name: supaglue-info-contact
  severity: warn
- description: List endpoints should support cursor-based pagination. GET operations on collection resources should document pagination parameters.
  given: $.paths[?(!@property.match(/_upsert|_search|_update|{.*}$/))].get.parameters
  name: supaglue-pagination-parameters
  severity: info
- description: Operations should document 400 Bad Request error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: supaglue-400-error-response
  severity: info
rules_file: rules/supaglue-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/rules/supaglue-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 6
  warn: 4
slug: supaglue-rules
source_filename: supaglue-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  supaglue-apikey-header-security:\n    description: >-\n      Supaglue APIs use x-api-key header authentication. All endpoints should\n      define security with the ApiKeyAuth scheme.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  supaglue-customer-id-header:\n    description: >-\n      Supaglue CRM, Engagement, and Ticketing API operations require a\n      x-customer-id header to identify the customer context. Operations\n      accessing customer data should document this parameter.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      function: truthy\n\n  supaglue-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[A-Z]\"\n\n  supaglue-operation-ids-camel-case:\n    description: Operation IDs should use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-zA-Z][a-zA-Z0-9]*$\"\n\n  supaglue-provider-name-header:\n    description: >-\n      Supaglue CRM and Engagement APIs require x-provider-name header to\n      route requests to the correct provider (e.g. salesforce, hubspot).\n      Should be documented in operation parameters.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters\"\n    then:\n      function: defined\n\n  supaglue-upsert-paths:\n    description: >-\n      Upsert operations use /_upsert subpath convention (e.g. /contacts/_upsert,\n      /accounts/_upsert). These should use POST method.\n    severity: info\n    given: \"$.paths[*~/_upsert].post\"\n    then:\n      function: truthy\n\n  supaglue-search-paths:\n    description:\
  \ >-\n      Search operations use /_search subpath convention (e.g. /contacts/_search).\n      These should use POST method with a request body.\n    severity: info\n    given: \"$.paths[*~/_search].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  supaglue-info-contact:\n    description: APIs must define contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  supaglue-pagination-parameters:\n    description: >-\n      List endpoints should support cursor-based pagination. GET operations\n      on collection resources should document pagination parameters.\n    severity: info\n    given: \"$.paths[?(!@property.match(/_upsert|_search|_update|{.*}$/))].get.parameters\"\n    then:\n      function: defined\n\n  supaglue-400-error-response:\n    description: Operations should document 400 Bad Request error responses\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    then:\n      field: \"400\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/supaglue/refs/heads/main/rules/supaglue-rules.yml
tags:
- CRM
- HRIS
- Unified API
- Open Source
- Integrations
- Sales Engagement
- Spectral
- Linting
- API Governance
---
