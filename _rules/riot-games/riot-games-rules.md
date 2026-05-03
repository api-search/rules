---
api_specs:
- filename: riot-games-league-of-legends-openapi.yml
  format: yaml
  label: League of Legends API
  slug: league-of-legends-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/riot-games/refs/heads/main/openapi/riot-games-league-of-legends-openapi.yml
categories:
- riot
description: Spectral linting rules defining API design standards and conventions for Riot Games.
layout: rules
name: Riot Games API Rules
provider_name: Riot Games
provider_slug: riot-games
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: riot-operation-summary-title-case
  severity: warn
- description: Operation IDs should be camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: riot-operation-id-camel-case
  severity: warn
- description: Tags must use Title Case
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: riot-tags-title-case
  severity: warn
- description: All operations must require X-Riot-Token API key
  given: $.paths[*][get,post,put,patch,delete]
  name: riot-must-have-api-key-security
  severity: error
- description: GET operations must return a 200 response
  given: $.paths[*].get
  name: riot-responses-must-include-200
  severity: error
- description: Operations must include 403 Forbidden response for API key errors
  given: $.paths[*][get,post,put,patch,delete].responses
  name: riot-must-have-403-response
  severity: warn
- description: Operations must include 404 Not Found response for resource lookups
  given: $.paths[*].get.responses
  name: riot-must-have-404-response
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]
  name: riot-path-parameters-required
  severity: error
- description: All servers must use HTTPS
  given: $.servers[*].url
  name: riot-servers-must-be-https
  severity: error
- description: Operations using encrypted IDs should document encryption in description
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name =~ /encrypted/i)]
  name: riot-encrypted-ids-in-descriptions
  severity: info
rules_file: rules/riot-games-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/riot-games/refs/heads/main/rules/riot-games-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: riot-games-rules
source_filename: riot-games-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  riot-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-zA-Z]* )*[A-Z][a-zA-Z]*$\"\n\n  riot-operation-id-camel-case:\n    description: Operation IDs should be camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  riot-tags-title-case:\n    description: Tags must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  riot-must-have-api-key-security:\n    description: All operations must require X-Riot-Token API key\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: security\n      function: defined\n\n  riot-responses-must-include-200:\n    description: GET operations must return a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  riot-must-have-403-response:\n    description: Operations must include 403 Forbidden response for API key errors\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"403\"\n      function: defined\n\n  riot-must-have-404-response:\n    description: Operations must include 404 Not Found response for resource lookups\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"404\"\n      function: defined\n\n  riot-path-parameters-required:\n    description: Path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'path')]\"\n    then:\n      field:\
  \ required\n      function: truthy\n\n  riot-servers-must-be-https:\n    description: All servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  riot-encrypted-ids-in-descriptions:\n    description: Operations using encrypted IDs should document encryption in description\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name =~ /encrypted/i)]\"\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/riot-games/refs/heads/main/rules/riot-games-rules.yml
tags:
- Esports
- Gaming
- League of Legends
- Legends of Runeterra
- Teamfight Tactics
- VALORANT
- Spectral
- Linting
- API Governance
---
