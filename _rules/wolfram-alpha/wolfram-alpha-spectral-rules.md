---
api_specs:
- filename: wolfram-alpha-llm-api-openapi.yml
  format: yaml
  label: Wolfram|Alpha LLM API
  slug: llm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/openapi/wolfram-alpha-llm-api-openapi.yml
- filename: wolfram-alpha-full-results-api-openapi.yml
  format: yaml
  label: Wolfram|Alpha Full Results API
  slug: full-results-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/openapi/wolfram-alpha-full-results-api-openapi.yml
- filename: wolfram-alpha-short-answers-api-openapi.yml
  format: yaml
  label: Wolfram|Alpha Short Answers API
  slug: short-answers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/openapi/wolfram-alpha-short-answers-api-openapi.yml
- filename: wolfram-alpha-simple-api-openapi.yml
  format: yaml
  label: Wolfram|Alpha Simple API
  slug: simple-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/openapi/wolfram-alpha-simple-api-openapi.yml
- filename: wolfram-alpha-spoken-results-api-openapi.yml
  format: yaml
  label: Wolfram|Alpha Spoken Results API
  slug: spoken-results-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/openapi/wolfram-alpha-spoken-results-api-openapi.yml
categories:
- delete
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- response
- security
- servers
- tag
description: Spectral linting rules defining API design standards and conventions for Wolfram|Alpha.
layout: rules
name: Wolfram|Alpha API Rules
provider_name: Wolfram|Alpha
provider_slug: wolfram-alpha
rule_count: 26
rules:
- description: API title must be present and start with "Wolfram|Alpha".
  given: $.info
  name: info-title-required
  severity: error
- description: API description must be present and at least 50 characters.
  given: $.info
  name: info-description-required
  severity: error
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information must be present.
  given: $.info
  name: info-contact-required
  severity: warn
- description: OpenAPI version must be 3.1.0.
  given: $
  name: openapi-version
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Paths must not have trailing slashes.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Query parameters must not be embedded in path strings.
  given: $.paths[*]~
  name: paths-query-params-not-in-path
  severity: error
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationid-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-operationid-camelcase
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Wolfram|Alpha ".
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-wolfram-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: All parameters must have descriptions.
  given: $.paths[*][get,post,put,patch,delete][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: The appid parameter description must mention Wolfram|Alpha AppID.
  given: $.paths[*][get].parameters[?(@.name == 'appid')]
  name: parameter-appid-required-description
  severity: info
- description: Operations must define at least a 200 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 400 error response.
  given: $.paths[*][get,post].responses
  name: response-error-400-defined
  severity: info
- description: Operations should define a 403 error response for auth-protected APIs.
  given: $.paths[*][get,post].responses
  name: response-error-403-defined
  severity: info
- description: Global tags must have descriptions.
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have request bodies.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have request bodies.
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Operations should provide examples for documentation and mocking.
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: operation-examples-encouraged
  severity: info
- description: Operations should include x-microcks-operation for mock server compatibility.
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
rules_file: rules/wolfram-alpha-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/rules/wolfram-alpha-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 5
  warn: 11
slug: wolfram-alpha-spectral-rules
source_filename: wolfram-alpha-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and start with \"Wolfram|Alpha\".\n    message: \"info.title must be present and start with 'Wolfram|Alpha'.\"\n    severity: error\n    given: $.info\n    then:\n      - field: title\n        function: truthy\n      - field: title\n        function: pattern\n        functionOptions:\n          match: \"^Wolfram\\\\|Alpha\"\n\n  info-description-required:\n    description: API description must be present and at least 50 characters.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        value: 50\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information must be present.\n    severity: warn\n    given: $.info\n    then:\n\
  \      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version:\n    description: OpenAPI version must be 3.1.0.\n    severity: warn\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS - NAMING CONVENTIONS\n  paths-no-trailing-slash:\n    description: Paths must not have trailing slashes.\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  paths-query-params-not-in-path:\n    description: Query\
  \ parameters must not be embedded in path strings.\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\?\"\n\n  # OPERATIONS\n  operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camelcase:\n    description: operationId must use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-wolfram-prefix:\n\
  \    description: Operation summaries must start with \"Wolfram|Alpha \".\n    message: \"Operation summary must start with 'Wolfram|Alpha '.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Wolfram\\\\|Alpha \"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have descriptions.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete][*].parameters[*]\"\
  \n    then:\n      field: description\n      function: truthy\n\n  parameter-appid-required-description:\n    description: The appid parameter description must mention Wolfram|Alpha AppID.\n    severity: info\n    given: \"$.paths[*][get].parameters[?(@.name == 'appid')]\"\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least a 200 success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  response-error-400-defined:\n    description: Operations should define a 400 error response.\n    severity: info\n    given: \"$.paths[*][get,post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['400']\n\n  response-error-403-defined:\n\
  \    description: Operations should define a 403 error response for auth-protected APIs.\n    severity: info\n    given: \"$.paths[*][get,post].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: ['403']\n\n  # TAGS\n  tag-description-required:\n    description: Global tags must have descriptions.\n    severity: warn\n    given: $.tags[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have request bodies.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have request bodies.\n    severity:\
  \ warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  operation-examples-encouraged:\n    description: Operations should provide examples for documentation and mocking.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*].content[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['example']\n            - required: ['examples']\n\n  microcks-operation-extension:\n    description: Operations should include x-microcks-operation for mock server compatibility.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wolfram-alpha/refs/heads/main/rules/wolfram-alpha-spectral-rules.yml
tags:
- AI
- Artificial Intelligence
- Computational Knowledge
- Natural Language Processing
- Search
- Spectral
- Linting
- API Governance
---
