---
api_specs:
- filename: index.htm
  format: yaml
  label: The Bureau of Economic Analysis API
  slug: the-bureau-of-economic-analysis
  spec_type: OpenAPI
  url: https://apps.bea.gov/API/docs/index.htm
categories:
- bea
description: Spectral linting rules defining API design standards and conventions for The Bureau of Economic Analysis.
layout: rules
name: The Bureau of Economic Analysis API Rules
provider_name: The Bureau of Economic Analysis
provider_slug: the-bureau-of-economic-analysis
rule_count: 10
rules:
- description: All BEA API operations must include a UserID query parameter for authentication.
  given: $.paths[*][get].parameters[*]
  name: bea-operation-must-have-userid-param
  severity: error
- description: All BEA API GET operations must include a 'method' query parameter specifying the API method to invoke.
  given: $.paths[*][get]
  name: bea-operation-must-have-method-param
  severity: error
- description: ResultFormat parameter must only accept JSON or XML values.
  given: $.paths[*][get].parameters[?(@.name == 'ResultFormat')].schema
  name: bea-result-format-enum
  severity: warn
- description: All operations must be tagged to organize by domain (Metadata, National Accounts, Regional, Industry, International).
  given: $.paths[*][get]
  name: bea-operations-must-have-tags
  severity: warn
- description: All operations must have a summary using Title Case.
  given: $.paths[*][get]
  name: bea-operations-must-have-summary
  severity: warn
- description: All BEA API operations must define a 200 success response.
  given: $.paths[*][get].responses
  name: bea-responses-must-include-200
  severity: error
- description: All BEA API operations should define a 400 error response for invalid request parameters.
  given: $.paths[*][get].responses
  name: bea-responses-must-include-400
  severity: warn
- description: The UserID parameter must be marked as required on all endpoints.
  given: $.paths[*][get].parameters[?(@.name == 'UserID')]
  name: bea-userid-must-be-required
  severity: error
- description: All parameters must have descriptions to aid API consumers.
  given: $.paths[*][get].parameters[*]
  name: bea-parameters-must-have-descriptions
  severity: warn
- description: The API info object should include contact information for developer support.
  given: $.info
  name: bea-info-must-have-contact
  severity: warn
rules_file: rules/the-bureau-of-economic-analysis-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/the-bureau-of-economic-analysis/refs/heads/main/rules/the-bureau-of-economic-analysis-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: the-bureau-of-economic-analysis-rules
source_filename: the-bureau-of-economic-analysis-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  bea-operation-must-have-userid-param:\n    description: All BEA API operations must include a UserID query parameter for authentication.\n    severity: error\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^UserID$\"\n\n  bea-operation-must-have-method-param:\n    description: All BEA API GET operations must include a 'method' query parameter specifying the API method to invoke.\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                type: string\n                enum: [\"method\"]\n              in:\n                type: string\n                enum: [\"query\"]\n\n  bea-result-format-enum:\n    description: ResultFormat\
  \ parameter must only accept JSON or XML values.\n    severity: warn\n    given: \"$.paths[*][get].parameters[?(@.name == 'ResultFormat')].schema\"\n    then:\n      field: enum\n      function: truthy\n\n  bea-operations-must-have-tags:\n    description: All operations must be tagged to organize by domain (Metadata, National Accounts, Regional, Industry, International).\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: tags\n      function: truthy\n\n  bea-operations-must-have-summary:\n    description: All operations must have a summary using Title Case.\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: summary\n      function: truthy\n\n  bea-responses-must-include-200:\n    description: All BEA API operations must define a 200 success response.\n    severity: error\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  bea-responses-must-include-400:\n    description: All BEA API\
  \ operations should define a 400 error response for invalid request parameters.\n    severity: warn\n    given: \"$.paths[*][get].responses\"\n    then:\n      field: \"400\"\n      function: truthy\n\n  bea-userid-must-be-required:\n    description: The UserID parameter must be marked as required on all endpoints.\n    severity: error\n    given: \"$.paths[*][get].parameters[?(@.name == 'UserID')]\"\n    then:\n      field: required\n      function: truthy\n\n  bea-parameters-must-have-descriptions:\n    description: All parameters must have descriptions to aid API consumers.\n    severity: warn\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  bea-info-must-have-contact:\n    description: The API info object should include contact information for developer support.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/the-bureau-of-economic-analysis/refs/heads/main/rules/the-bureau-of-economic-analysis-rules.yml
tags:
- Economics
- Federal Government
- GDP
- National Accounts
- Open Data
- Statistics
- Spectral
- Linting
- API Governance
---
