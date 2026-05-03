---
categories:
- cloudera
description: Spectral linting rules defining API design standards and conventions for Cloudera.
layout: rules
name: Cloudera API Rules
provider_name: Cloudera
provider_slug: cloudera
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudera-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudera-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudera-server-https
  severity: error
- description: Cloudera Manager paths must be versioned (/api/v{N}).
  given: $.servers[?(@.url && @.url.indexOf('cloudera') > -1)].url
  name: cloudera-cm-versioned
  severity: warn
- description: A security scheme (basic or apiKey) must be declared.
  given: $.components.securitySchemes
  name: cloudera-auth-required
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudera-operation-tags
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudera-operation-id
  severity: error
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudera-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudera-error-responses
  severity: warn
rules_file: rules/cloudera-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudera/refs/heads/main/rules/cloudera-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: cloudera-rules
source_filename: cloudera-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for Cloudera CDP / Cloudera Manager APIs.\nrules:\n  cloudera-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cloudera-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cloudera-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cloudera-cm-versioned:\n    description: Cloudera Manager paths must be versioned (/api/v{N}).\n    severity: warn\n    given: \"$.servers[?(@.url && @.url.indexOf('cloudera') > -1)].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/api/v\\\\d+(/|$)\"\n\n  cloudera-auth-required:\n\
  \    description: A security scheme (basic or apiKey) must be declared.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  cloudera-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cloudera-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cloudera-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cloudera-error-responses:\n    description: Mutating\
  \ operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudera/refs/heads/main/rules/cloudera-rules.yml
tags:
- Big Data
- Data Engineering
- Data Lakehouse
- Data Platform
- Data Warehouse
- Hadoop
- Hybrid Cloud
- Machine Learning
- Streaming
- Spectral
- Linting
- API Governance
---
