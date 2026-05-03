---
api_specs:
- filename: usace-cwms-data-api-openapi.yml
  format: yaml
  label: USACE Corps Water Management System Data API
  slug: cwms-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-department-of-defense/refs/heads/main/openapi/usace-cwms-data-api-openapi.yml
categories:
- cwms
description: Spectral linting rules defining API design standards and conventions for US Department of Defense.
layout: rules
name: US Department of Defense API Rules
provider_name: US Department of Defense
provider_slug: us-department-of-defense
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: cwms-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: cwms-operations-have-summaries
  severity: error
- description: All operations should be tagged for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: cwms-operations-have-tags
  severity: warn
- description: Office parameter should have a description explaining valid values
  given: $.paths[*][*].parameters[?(@.name == 'office')]
  name: cwms-office-param-described
  severity: info
- description: All GET operations should define a 200 response
  given: $.paths[*][get]
  name: cwms-response-200-defined
  severity: warn
- description: API must define servers for base URL
  given: $
  name: cwms-servers-defined
  severity: error
- description: API should have contact information
  given: $.info
  name: cwms-info-contact-present
  severity: warn
- description: Tags must use Title Case naming
  given: $.tags[*].name
  name: cwms-tags-title-case
  severity: warn
- description: Time parameters should specify ISO 8601 format
  given: $.paths[*][*].parameters[?(@.name == 'begin' || @.name == 'end')]
  name: cwms-time-params-iso8601
  severity: info
- description: API paths should use lowercase
  given: $.paths
  name: cwms-path-lowercase
  severity: warn
rules_file: rules/usace-cwms-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-department-of-defense/refs/heads/main/rules/usace-cwms-data-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 6
slug: usace-cwms-data-api-rules
source_filename: usace-cwms-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  cwms-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: Operation ID \"{{value}}\" should use camelCase (e.g., getTimeSeries, getLocations)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  cwms-operations-have-summaries:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cwms-operations-have-tags:\n    description: All operations should be tagged for grouping\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  cwms-office-param-described:\n    description: Office parameter should\
  \ have a description explaining valid values\n    message: Query parameter 'office' should have a description\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'office')]\"\n    then:\n      field: description\n      function: truthy\n\n  cwms-response-200-defined:\n    description: All GET operations should define a 200 response\n    message: GET operation is missing a 200 OK response definition\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  cwms-servers-defined:\n    description: API must define servers for base URL\n    message: No servers defined in the API specification\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  cwms-info-contact-present:\n    description: API should have contact information\n    message: API info is missing contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function:\
  \ truthy\n\n  cwms-tags-title-case:\n    description: Tags must use Title Case naming\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n\n  cwms-time-params-iso8601:\n    description: Time parameters should specify ISO 8601 format\n    message: Time parameter should specify format in description\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'begin' || @.name == 'end')]\"\n    then:\n      field: description\n      function: truthy\n\n  cwms-path-lowercase:\n    description: API paths should use lowercase\n    message: Path should be lowercase\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z\\\\/\\\\{\\\\}\\\\-]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-department-of-defense/refs/heads/main/rules/usace-cwms-data-api-rules.yml
tags:
- Federal Government
- Defense
- Military
- Water Management
- Waterways
- Open Data
- Spectral
- Linting
- API Governance
---
