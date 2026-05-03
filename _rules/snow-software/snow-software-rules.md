---
api_specs:
- filename: snow-software-licenses-openapi.yml
  format: yaml
  label: Snow Atlas SAM Licenses API
  slug: snow-atlas-licenses-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/openapi/snow-software-licenses-openapi.yml
- filename: snow-software-saas-applications-openapi.yml
  format: yaml
  label: Snow Atlas SaaS Applications API
  slug: snow-atlas-saas-applications-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/openapi/snow-software-saas-applications-openapi.yml
- filename: snow-software-saas-subscriptions-openapi.yml
  format: yaml
  label: Snow Atlas SaaS Subscriptions API
  slug: snow-atlas-saas-subscriptions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/openapi/snow-software-saas-subscriptions-openapi.yml
- filename: snow-software-computers-openapi.json
  format: json
  label: Snow Atlas SAM Computers API
  slug: snow-atlas-computers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/openapi/snow-software-computers-openapi.json
categories:
- snow
description: Spectral linting rules defining API design standards and conventions for Snow Software.
layout: rules
name: Snow Software API Rules
provider_name: Snow Software
provider_slug: snow-software
rule_count: 9
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][*].operationId
  name: snow-operation-id-camel-case
  severity: warn
- description: Snow Atlas server URLs should include a {region} variable for multi-region support
  given: $.servers[*].url
  name: snow-server-region-variable
  severity: warn
- description: Collection endpoints should support page_number and page_size parameters
  given: $.paths[*].get.parameters[*].name
  name: snow-pagination-params
  severity: info
- description: Snow Atlas APIs should support filter query parameters for collection endpoints
  given: $.paths[*].get
  name: snow-filter-param
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: snow-operation-tag
  severity: warn
- description: All operations must have a summary in Title Case
  given: $.paths[*][get,post,put,delete,patch]
  name: snow-operation-summary
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: snow-operation-description
  severity: info
- description: Snow Atlas collection responses follow a HATEOAS pattern with pagination links
  given: $.paths[*][get].responses['200'].content['application/json'].schema
  name: snow-hateoas-response
  severity: info
- description: Operations should define a 400 Bad Request response
  given: $.paths[*][post,put,patch].responses
  name: snow-400-error-defined
  severity: info
rules_file: rules/snow-software-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/rules/snow-software-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 5
  warn: 4
slug: snow-software-rules
source_filename: snow-software-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation naming\n  snow-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: \"operationId '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Region variable in server\n  snow-server-region-variable:\n    description: Snow Atlas server URLs should include a {region} variable for multi-region support\n    message: \"Server URL should include {region} variable for Snow Atlas multi-region\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{region\\\\}.*\"\n\n  # Pagination parameters\n  snow-pagination-params:\n    description: Collection endpoints should support page_number and page_size parameters\n    message: \"Collection GET operations should support\
  \ pagination parameters\"\n    severity: info\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(page_number|page_size|filter|sort)$\"\n\n  # Filter parameter\n  snow-filter-param:\n    description: Snow Atlas APIs should support filter query parameters for collection endpoints\n    message: \"Collection GET endpoints should support a filter parameter\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  # Tag requirements\n  snow-operation-tag:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Summary requirements\n  snow-operation-summary:\n    description: All operations must have a summary in Title Case\n    message: \"Operation must have a summary\"\
  \n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Description requirements\n  snow-operation-description:\n    description: All operations should have a description\n    message: \"Operation should have a description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  # HATEOAS response pattern\n  snow-hateoas-response:\n    description: Snow Atlas collection responses follow a HATEOAS pattern with pagination links\n    message: \"200 response should have a defined schema\"\n    severity: info\n    given: \"$.paths[*][get].responses['200'].content['application/json'].schema\"\n    then:\n      function: truthy\n\n  # Error response definitions\n  snow-400-error-defined:\n    description: Operations should define a 400 Bad Request response\n    message: \"Operation should define a 400 response\"\n    severity:\
  \ info\n    given: \"$.paths[*][post,put,patch].responses\"\n    then:\n      field: \"400\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/snow-software/refs/heads/main/rules/snow-software-rules.yml
tags:
- Cloud License Management
- FinOps
- IT Asset Management
- SaaS Management
- Software Asset Management
- Spectral
- Linting
- API Governance
---
