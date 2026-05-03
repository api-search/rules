---
categories:
- sherwin
description: Spectral linting rules defining API design standards and conventions for Sherwin-Williams.
layout: rules
name: Sherwin-Williams API Rules
provider_name: Sherwin-Williams
provider_slug: sherwin-williams
rule_count: 7
rules:
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sherwin-williams-must-have-summary
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: sherwin-williams-must-have-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sherwin-williams-must-have-operation-id
  severity: error
- description: Paths must not have trailing slashes
  given: $.paths
  name: sherwin-williams-no-trailing-slash
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: sherwin-williams-operation-id-camel-case
  severity: warn
- description: All parameters must have a schema defined
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: sherwin-williams-parameters-have-schema
  severity: error
- description: B2B APIs must have authentication defined
  given: $.security
  name: sherwin-williams-b2b-auth
  severity: error
rules_file: rules/sherwin-williams-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sherwin-williams/refs/heads/main/rules/sherwin-williams-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 2
slug: sherwin-williams-rules
source_filename: sherwin-williams-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Sherwin-Williams API Governance Rules\n  sherwin-williams-must-have-summary:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  sherwin-williams-must-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  sherwin-williams-must-have-operation-id:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  sherwin-williams-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\
  .*/$\"\n\n  sherwin-williams-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sherwin-williams-parameters-have-schema:\n    description: All parameters must have a schema defined\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: defined\n\n  sherwin-williams-b2b-auth:\n    description: B2B APIs must have authentication defined\n    severity: error\n    given: \"$.security\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sherwin-williams/refs/heads/main/rules/sherwin-williams-rules.yml
tags:
- B2B
- Construction
- Fortune 500
- Paints
- Retail
- Supply Chain
- Spectral
- Linting
- API Governance
---
