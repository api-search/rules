---
api_specs:
- filename: sam-gov-location-services-openapi.yml
  format: yaml
  label: SAM.gov Public Location Services API
  slug: location-services-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sam.gov/refs/heads/main/openapi/sam-gov-location-services-openapi.yml
categories:
- sam
description: Spectral linting rules defining API design standards and conventions for SAM.gov.
layout: rules
name: SAM.gov API Rules
provider_name: SAM.gov
provider_slug: sam.gov
rule_count: 10
rules:
- description: SAM.gov APIs require an api_key query parameter
  given: $.paths[*][get,post,put,patch,delete]
  name: sam-gov-api-key-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sam-gov-summary-title-case
  severity: warn
- description: Operations must have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: sam-gov-operation-description
  severity: warn
- description: Operations must define responses
  given: $.paths[*][get,post,put,patch,delete]
  name: sam-gov-responses-required
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: sam-gov-get-200-response
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sam-gov-operation-tags
  severity: warn
- description: API must define servers
  given: $
  name: sam-gov-servers-defined
  severity: error
- description: Info section must be complete
  given: $.info
  name: sam-gov-info-complete
  severity: error
- description: API paths should use kebab-case
  given: $.paths
  name: sam-gov-path-kebab-case
  severity: hint
- description: Parameters must have descriptions
  given: $.paths[*][*].parameters[*].name
  name: sam-gov-parameter-descriptions
  severity: hint
rules_file: rules/sam-gov-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sam.gov/refs/heads/main/rules/sam-gov-rules.yml
severity_counts:
  error: 4
  hint: 2
  info: 0
  warn: 4
slug: sam-gov-rules
source_filename: sam-gov-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # SAM.gov API key is required on all operations\n  sam-gov-api-key-required:\n    description: SAM.gov APIs require an api_key query parameter\n    message: \"Operation '{{path}}' must include an api_key query parameter\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - field: parameters\n        function: truthy\n    severity: error\n\n  # All operations must have summaries in Title Case\n  sam-gov-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n    severity: warn\n\n  # All operations must have descriptions\n  sam-gov-operation-description:\n    description: Operations must have descriptions\n    message: \"Operation at '{{path}}' must have a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      - field: description\n        function: truthy\n    severity: warn\n\n  # Responses must be defined\n  sam-gov-responses-required:\n    description: Operations must define responses\n    message: \"Operation at '{{path}}' must define responses\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - field: responses\n        function: truthy\n    severity: error\n\n  # GET operations should return 200\n  sam-gov-get-200-response:\n    description: GET operations must define a 200 response\n    message: \"GET operation at '{{path}}' should have a 200 response\"\n    given: \"$.paths[*].get\"\n    then:\n      - field: responses.200\n        function: truthy\n    severity: warn\n\n  # Operations must have tags\n  sam-gov-operation-tags:\n    description: Operations must have at least one tag\n    message: \"Operation at '{{path}}' must have at least one tag\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      - field: tags\n    \
  \    function: truthy\n    severity: warn\n\n  # Server URL must be defined\n  sam-gov-servers-defined:\n    description: API must define servers\n    message: \"API must have servers defined\"\n    given: \"$\"\n    then:\n      - field: servers\n        function: truthy\n    severity: error\n\n  # Info section must be complete\n  sam-gov-info-complete:\n    description: Info section must be complete\n    message: \"API info must have a title, description, and version\"\n    given: \"$.info\"\n    then:\n      - field: title\n        function: truthy\n      - field: description\n        function: truthy\n      - field: version\n        function: truthy\n    severity: error\n\n  # Paths should use kebab-case\n  sam-gov-path-kebab-case:\n    description: API paths should use kebab-case\n    message: \"Path '{{path}}' should use kebab-case\"\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/[a-z0-9/{}\\\\-]+$\"\n    severity: hint\n\
  \n  # Parameters must have descriptions\n  sam-gov-parameter-descriptions:\n    description: Parameters must have descriptions\n    message: \"Parameter '{{value}}' must have a description\"\n    given: \"$.paths[*][*].parameters[*].name\"\n    then:\n      function: truthy\n    severity: hint\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sam.gov/refs/heads/main/rules/sam-gov-rules.yml
tags:
- Federal Government
- Procurement
- Contracts
- Entity Management
- Location Services
- GSA
- Spectral
- Linting
- API Governance
---
