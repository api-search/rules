---
api_specs:
- filename: whmcs-openapi.yml
  format: yaml
  label: WHMCS API
  slug: whmcs
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/whmcs/main/openapi/whmcs-openapi.yml
categories:
- whmcs
description: Spectral linting rules defining API design standards and conventions for WHMCS.
layout: rules
name: WHMCS API Rules
provider_name: WHMCS
provider_slug: whmcs
rule_count: 10
rules:
- description: All WHMCS API paths must include an ?action= query parameter identifying the operation.
  given: $.paths[*]~
  name: whmcs-path-must-include-action
  severity: error
- description: WHMCS operation IDs must use camelCase to match the API command naming convention.
  given: $.paths[*][*].operationId
  name: whmcs-operation-id-camel-case
  severity: warn
- description: All WHMCS API operations must use POST method. WHMCS does not support GET, PUT, or DELETE.
  given: $.paths[*]
  name: whmcs-post-only
  severity: error
- description: All WHMCS API operations must reference the AuthCredentials schema for authentication.
  given: $.paths[*].post.requestBody.content['application/x-www-form-urlencoded'].schema
  name: whmcs-auth-required
  severity: error
- description: WHMCS API responses must support application/json content type.
  given: $.paths[*].post.responses[*].content
  name: whmcs-response-json
  severity: warn
- description: All WHMCS API operations must have a summary in Title Case.
  given: $.paths[*].post.summary
  name: whmcs-operation-summary-required
  severity: warn
- description: All WHMCS API operations must have at least one tag for categorization.
  given: $.paths[*].post.tags
  name: whmcs-operation-tags-required
  severity: warn
- description: WHMCS API request bodies must use application/x-www-form-urlencoded content type.
  given: $.paths[*].post.requestBody.content
  name: whmcs-request-form-urlencoded
  severity: error
- description: All WHMCS API responses must include a 'result' field indicating success or error.
  given: $.components.schemas[*].properties
  name: whmcs-response-result-field
  severity: warn
- description: WHMCS API spec must include a version in the info object.
  given: $.info.version
  name: whmcs-info-version-required
  severity: error
rules_file: rules/whmcs-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/whmcs/refs/heads/main/rules/whmcs-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: whmcs-rules
source_filename: whmcs-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # WHMCS uses POST with ?action= query param for all operations\n  whmcs-path-must-include-action:\n    description: All WHMCS API paths must include an ?action= query parameter identifying the operation.\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\?action=[A-Za-z]+\"\n\n  # Operation IDs must use camelCase\n  whmcs-operation-id-camel-case:\n    description: WHMCS operation IDs must use camelCase to match the API command naming convention.\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must use POST (WHMCS is POST-only)\n  whmcs-post-only:\n    description: All WHMCS API operations must use POST method. WHMCS does not support GET, PUT, or DELETE.\n    severity: error\n    given: \"$.paths[*]\"\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - post\n          not:\n            anyOf:\n              - required: [get]\n              - required: [put]\n              - required: [delete]\n              - required: [patch]\n\n  # All operations must have authentication credentials in request body\n  whmcs-auth-required:\n    description: All WHMCS API operations must reference the AuthCredentials schema for authentication.\n    severity: error\n    given: \"$.paths[*].post.requestBody.content['application/x-www-form-urlencoded'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            allOf:\n              type: array\n\n  # Responses must use application/json\n  whmcs-response-json:\n    description: WHMCS API responses must support application/json content type.\n    severity: warn\n    given: \"$.paths[*].post.responses[*].content\"\
  \n    then:\n      function: truthy\n\n  # Operations must have summaries\n  whmcs-operation-summary-required:\n    description: All WHMCS API operations must have a summary in Title Case.\n    severity: warn\n    given: \"$.paths[*].post.summary\"\n    then:\n      function: truthy\n\n  # All operations must be tagged\n  whmcs-operation-tags-required:\n    description: All WHMCS API operations must have at least one tag for categorization.\n    severity: warn\n    given: \"$.paths[*].post.tags\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  # RequestBody must be form-urlencoded\n  whmcs-request-form-urlencoded:\n    description: WHMCS API request bodies must use application/x-www-form-urlencoded content type.\n    severity: error\n    given: \"$.paths[*].post.requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n   \
  \         - \"application/x-www-form-urlencoded\"\n\n  # All response schemas must include a 'result' field\n  whmcs-response-result-field:\n    description: All WHMCS API responses must include a 'result' field indicating success or error.\n    severity: warn\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: truthy\n\n  # API version must be documented\n  whmcs-info-version-required:\n    description: WHMCS API spec must include a version in the info object.\n    severity: error\n    given: \"$.info.version\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/whmcs/refs/heads/main/rules/whmcs-rules.yml
tags:
- Web Hosting
- Billing Automation
- Client Management
- Domain Management
- Support Tickets
- Provisioning
- Spectral
- Linting
- API Governance
---
