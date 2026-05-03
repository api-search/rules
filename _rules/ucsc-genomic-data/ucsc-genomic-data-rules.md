---
api_specs:
- filename: ucsc-genomic-data-openapi.yml
  format: yaml
  label: UCSC Genome Browser REST API
  slug: ucsc-genomic-data
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ucsc-genomic-data/refs/heads/main/openapi/ucsc-genomic-data-openapi.yml
categories:
- ucsc
description: Spectral linting rules defining API design standards and conventions for UCSC Genomic Data.
layout: rules
name: UCSC Genomic Data API Rules
provider_name: UCSC Genomic Data
provider_slug: ucsc-genomic-data
rule_count: 6
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: ucsc-has-operation-id
  severity: error
- description: Operation IDs must use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: ucsc-operation-id-camel-case
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: ucsc-has-description
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: ucsc-has-tags
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: ucsc-summary-title-case
  severity: warn
- description: GET operations should define a response schema for 200.
  given: $.paths[*].get.responses.200
  name: ucsc-get-has-response-schema
  severity: warn
rules_file: rules/ucsc-genomic-data-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ucsc-genomic-data/refs/heads/main/rules/ucsc-genomic-data-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 5
slug: ucsc-genomic-data-rules
source_filename: ucsc-genomic-data-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ucsc-has-operation-id:\n    description: All operations must have an operationId.\n    message: Operation is missing operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  ucsc-operation-id-camel-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ucsc-has-description:\n    description: All operations must have a description.\n    message: Operation is missing a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  ucsc-has-tags:\n    description: All operations must have at least one tag.\n\
  \    message: Operation is missing tags.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  ucsc-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  ucsc-get-has-response-schema:\n    description: GET operations should define a response schema for 200.\n    message: GET 200 response at '{{path}}' should define a content schema.\n    severity: warn\n    given: \"$.paths[*].get.responses.200\"\n    then:\n      field: content\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ucsc-genomic-data/refs/heads/main/rules/ucsc-genomic-data-rules.yml
tags:
- Genomics
- Bioinformatics
- DNA
- Biology
- Research
- Open Science
- Spectral
- Linting
- API Governance
---
