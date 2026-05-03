---
api_specs:
- filename: talend-orchestration-openapi.yml
  format: yaml
  label: Talend Cloud Orchestration API
  slug: talend-orchestration-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/talend/refs/heads/main/openapi/talend-orchestration-openapi.yml
- filename: talend-processing-openapi.yml
  format: yaml
  label: Talend Cloud Processing API
  slug: talend-processing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/talend/refs/heads/main/openapi/talend-processing-openapi.yml
categories:
- talend
description: Spectral linting rules defining API design standards and conventions for Talend.
layout: rules
name: Talend API Rules
provider_name: Talend
provider_slug: talend
rule_count: 9
rules:
- description: All Talend API operations must have operationIds
  given: $.paths[*][get,post,put,patch,delete]
  name: talend-operations-have-operation-ids
  severity: error
- description: All operations must have summaries
  given: $.paths[*][get,post,put,patch,delete]
  name: talend-operations-have-summaries
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: talend-operations-have-tags
  severity: warn
- description: API must use Bearer authentication (not API key)
  given: $.components.securitySchemes
  name: talend-bearer-auth-required
  severity: warn
- description: Path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: talend-path-params-have-descriptions
  severity: warn
- description: ID fields in schemas must be type string
  given: $.components.schemas[*].properties.id
  name: talend-ids-are-strings
  severity: error
- description: Timestamp fields should use format date-time
  given: $.components.schemas[*].properties[created,updated,startTime,endTime]
  name: talend-timestamps-use-date-time
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: talend-delete-returns-204
  severity: info
- description: Status fields should have enum values defined
  given: $.components.schemas[*].properties.status
  name: talend-status-fields-have-enums
  severity: info
rules_file: rules/talend-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/talend/refs/heads/main/rules/talend-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: talend-api-rules
source_filename: talend-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  talend-operations-have-operation-ids:\n    description: All Talend API operations must have operationIds\n    message: \"Operation at '{{path}}' is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  talend-operations-have-summaries:\n    description: All operations must have summaries\n    message: \"Operation '{{property}}' is missing a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  talend-operations-have-tags:\n    description: All operations must have at least one tag\n    message: \"Operation should have at least one tag for grouping\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  talend-bearer-auth-required:\n    description: API must use Bearer\
  \ authentication (not API key)\n    message: \"Talend APIs use Bearer token authentication\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  talend-path-params-have-descriptions:\n    description: Path parameters must have descriptions\n    message: \"Path parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  talend-ids-are-strings:\n    description: ID fields in schemas must be type string\n    message: \"ID field should be type: string\"\n    severity: error\n    given: \"$.components.schemas[*].properties.id\"\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\n  talend-timestamps-use-date-time:\n    description: Timestamp fields should use format date-time\n    message: \"Timestamp field '{{property}}' should\
  \ use format: date-time\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[created,updated,startTime,endTime]\"\n    then:\n      field: format\n      function: pattern\n      functionOptions:\n        match: \"^date-time$\"\n\n  talend-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: \"DELETE operations should include a 204 response\"\n    severity: info\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  talend-status-fields-have-enums:\n    description: Status fields should have enum values defined\n    message: \"Status field should define allowed enum values\"\n    severity: info\n    given: \"$.components.schemas[*].properties.status\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/talend/refs/heads/main/rules/talend-api-rules.yml
tags:
- API Management
- Data Integration
- Data Quality
- ETL
- Orchestration
- Pipelines
- Spectral
- Linting
- API Governance
---
