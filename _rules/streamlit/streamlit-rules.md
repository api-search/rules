---
api_specs:
- filename: streamlit-cloud-openapi.yml
  format: yaml
  label: Streamlit Community Cloud API
  slug: streamlit-cloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/streamlit/refs/heads/main/openapi/streamlit-cloud-openapi.yml
categories:
- streamlit
description: Spectral linting rules defining API design standards and conventions for Streamlit.
layout: rules
name: Streamlit API Rules
provider_name: Streamlit
provider_slug: streamlit
rule_count: 8
rules:
- description: Streamlit Cloud API operationIds use camelCase (e.g., listApps, deployApp, getApp, restartApp).
  given: $.paths[*][*].operationId
  name: streamlit-operation-ids-camel-case
  severity: warn
- description: All OpenAPI tags must use Title Case (e.g., 'Apps', 'Secrets', 'Workspaces').
  given: $.tags[*].name
  name: streamlit-tags-title-case
  severity: warn
- description: All Streamlit Cloud API endpoints require Bearer token authentication.
  given: $.components.securitySchemes
  name: streamlit-bearer-auth
  severity: warn
- description: App-specific endpoints use appId as the path parameter name for the application identifier.
  given: $.paths['/apps/{appId}'][*].parameters[*]
  name: streamlit-app-id-path-param
  severity: warn
- description: 'The Streamlit Cloud API never returns secret values, only key names. Security review: verify no secret values appear in response schemas.'
  given: $.paths['/apps/{appId}/secrets'][get].responses['200'].content['application/json'].schema
  name: streamlit-secrets-never-returned
  severity: error
- description: DELETE operations in Streamlit Cloud API return 204 No Content on successful deletion.
  given: $.paths[*][delete].responses
  name: streamlit-delete-returns-204
  severity: info
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: streamlit-operation-summaries-present
  severity: error
- description: List endpoints should support consistent pagination parameters (page and per_page).
  given: $.paths['/apps'][get].parameters[*].name
  name: streamlit-pagination-consistent
  severity: info
rules_file: rules/streamlit-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/streamlit/refs/heads/main/rules/streamlit-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: streamlit-rules
source_filename: streamlit-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  streamlit-operation-ids-camel-case:\n    description: >-\n      Streamlit Cloud API operationIds use camelCase (e.g., listApps,\n      deployApp, getApp, restartApp).\n    message: \"OperationId '{{value}}' must use camelCase format\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  streamlit-tags-title-case:\n    description: >-\n      All OpenAPI tags must use Title Case (e.g., 'Apps', 'Secrets', 'Workspaces').\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  streamlit-bearer-auth:\n    description: >-\n      All Streamlit Cloud API endpoints require Bearer token authentication.\n    message: \"API must use streamlitBearerAuth security scheme\"\
  \n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: \"streamlitBearerAuth\"\n\n  streamlit-app-id-path-param:\n    description: >-\n      App-specific endpoints use appId as the path parameter name for\n      the application identifier.\n    message: \"App path parameter must be named 'appId'\"\n    severity: warn\n    given: \"$.paths['/apps/{appId}'][*].parameters[*]\"\n    then:\n      field: \"name\"\n      function: enumeration\n      functionOptions:\n        values:\n          - appId\n\n  streamlit-secrets-never-returned:\n    description: >-\n      The Streamlit Cloud API never returns secret values, only key names.\n      Security review: verify no secret values appear in response schemas.\n    message: \"Secrets response must not include actual secret values — only key names\"\n    severity: error\n    given: \"$.paths['/apps/{appId}/secrets'][get].responses['200'].content['application/json'].schema\"\n    then:\n\
  \      function: truthy\n\n  streamlit-delete-returns-204:\n    description: >-\n      DELETE operations in Streamlit Cloud API return 204 No Content\n      on successful deletion.\n    message: \"DELETE operation should return 204 on success\"\n    severity: info\n    given: \"$.paths[*][delete].responses\"\n    then:\n      function: truthy\n      field: \"204\"\n\n  streamlit-operation-summaries-present:\n    description: >-\n      All operations must have a summary.\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: truthy\n      field: \"summary\"\n\n  streamlit-pagination-consistent:\n    description: >-\n      List endpoints should support consistent pagination parameters\n      (page and per_page).\n    message: \"List endpoints should document page and per_page parameters\"\n    severity: info\n    given: \"$.paths['/apps'][get].parameters[*].name\"\n    then:\n      function: enumeration\n\
  \      functionOptions:\n        values:\n          - page\n          - per_page\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/streamlit/refs/heads/main/rules/streamlit-rules.yml
tags:
- Data Science
- Machine Learning
- Open Source
- Python
- Web Applications
- Spectral
- Linting
- API Governance
---
