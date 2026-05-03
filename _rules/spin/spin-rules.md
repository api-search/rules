---
categories:
- spin
description: Spectral linting rules defining API design standards and conventions for Spin.
layout: rules
name: Spin API Rules
provider_name: Spin
provider_slug: spin
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spin-operation-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: spin-tags-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-operation-id
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-operation-tags
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: spin-operation-description
  severity: warn
- description: All schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: spin-schema-descriptions
  severity: warn
- description: API info should include contact details
  given: $.info
  name: spin-info-contact
  severity: warn
rules_file: rules/spin-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spin/refs/heads/main/rules/spin-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: spin-rules
source_filename: spin-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spin-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: Operation summary \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spin-tags-title-case:\n    description: All tags must use Title Case\n    message: Tag \"{{value}}\" should be in Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  spin-operation-id:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spin-operation-tags:\n    description:\
  \ All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spin-operation-description:\n    description: All operations should have a description\n    message: Operation should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  spin-schema-descriptions:\n    description: All schema properties should have descriptions\n    message: Schema property should have a description\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spin-info-contact:\n    description: API info should include contact details\n    message: API info should have a contact object with url\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n\
  \      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spin/refs/heads/main/rules/spin-rules.yml
tags:
- Cloud Native
- Microservices
- Serverless
- WebAssembly
- Spectral
- Linting
- API Governance
---
