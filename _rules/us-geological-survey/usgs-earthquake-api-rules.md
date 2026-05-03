---
api_specs:
- filename: usgs-earthquake-catalog-openapi.yml
  format: yaml
  label: USGS Earthquake Catalog API
  slug: earthquake-catalog-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-geological-survey/refs/heads/main/openapi/usgs-earthquake-catalog-openapi.yml
- filename: openapi
  format: yaml
  label: USGS Water Data OGC API
  slug: water-data-api
  spec_type: OpenAPI
  url: https://api.waterdata.usgs.gov/ogcapi/v0/openapi?f=json
categories:
- usgs
description: Spectral linting rules defining API design standards and conventions for US Geological Survey.
layout: rules
name: US Geological Survey API Rules
provider_name: US Geological Survey
provider_slug: us-geological-survey
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: usgs-operation-ids-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: usgs-operations-have-summaries
  severity: error
- description: All operations should be tagged for grouping
  given: $.paths[*][get,post,put,patch,delete]
  name: usgs-operations-have-tags
  severity: warn
- description: Format parameters should list valid values
  given: $.paths[*][*].parameters[?(@.name == 'format')]
  name: usgs-format-param-documented
  severity: info
- description: All GET operations should define a 200 response
  given: $.paths[*][get]
  name: usgs-response-200-defined
  severity: warn
- description: Query operations should define a 400 bad request response
  given: $.paths[*][get]
  name: usgs-response-400-defined
  severity: info
- description: API must define servers
  given: $
  name: usgs-servers-defined
  severity: error
- description: Time parameters should indicate ISO 8601 format
  given: $.paths[*][*].parameters[?(@.name == 'starttime' || @.name == 'endtime')]
  name: usgs-time-params-iso8601-format
  severity: info
- description: Latitude parameters should specify valid range
  given: $.paths[*][*].parameters[?(@.name == 'minlatitude' || @.name == 'maxlatitude')]
  name: usgs-geo-params-in-range
  severity: info
- description: Tags must use Title Case naming
  given: $.tags[*].name
  name: usgs-tags-title-case
  severity: warn
rules_file: rules/usgs-earthquake-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-geological-survey/refs/heads/main/rules/usgs-earthquake-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 4
slug: usgs-earthquake-api-rules
source_filename: usgs-earthquake-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  usgs-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: Operation ID \"{{value}}\" should use camelCase (e.g., queryEarthquakes, countEarthquakes)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  usgs-operations-have-summaries:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  usgs-operations-have-tags:\n    description: All operations should be tagged for grouping\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  usgs-format-param-documented:\n    description: Format parameters\
  \ should list valid values\n    message: Format parameter should specify valid enum values\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'format')]\"\n    then:\n      field: schema.enum\n      function: truthy\n\n  usgs-response-200-defined:\n    description: All GET operations should define a 200 response\n    message: GET operation is missing a 200 OK response\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  usgs-response-400-defined:\n    description: Query operations should define a 400 bad request response\n    message: Operation should define a 400 response for invalid parameters\n    severity: info\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.400\n      function: truthy\n\n  usgs-servers-defined:\n    description: API must define servers\n    message: No servers defined\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\
  \n  usgs-time-params-iso8601-format:\n    description: Time parameters should indicate ISO 8601 format\n    message: Time parameter should document ISO 8601 date-time format\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'starttime' || @.name == 'endtime')]\"\n    then:\n      field: schema.format\n      function: truthy\n\n  usgs-geo-params-in-range:\n    description: Latitude parameters should specify valid range\n    message: Latitude parameter should specify minimum/maximum constraints\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'minlatitude' || @.name == 'maxlatitude')]\"\n    then:\n      field: schema.minimum\n      function: truthy\n\n  usgs-tags-title-case:\n    description: Tags must use Title Case naming\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-geological-survey/refs/heads/main/rules/usgs-earthquake-api-rules.yml
tags:
- Federal Government
- Earth Science
- Earthquakes
- Water Data
- Geospatial
- Hazards
- Environment
- Spectral
- Linting
- API Governance
---
