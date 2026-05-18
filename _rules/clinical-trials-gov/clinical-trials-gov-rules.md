---
categories:
- ctg
description: Spectral linting rules defining API design standards and conventions for ClinicalTrials.gov.
layout: rules
name: ClinicalTrials.gov API Rules
provider_name: ClinicalTrials.gov
provider_slug: clinical-trials-gov
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: ctg-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: ctg-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: ctg-server-https
  severity: error
- description: Data API server URL must include /api/v2.
  given: $.servers[?(@.url && @.url.indexOf('clinicaltrials.gov') > -1)].url
  name: ctg-server-versioned
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: ctg-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: ctg-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: ctg-operation-id
  severity: error
- description: List endpoints should support pageSize and pageToken parameters.
  given: $.paths[?(@property == '/studies')].get.parameters[*].name
  name: ctg-pagination-page-size
  severity: info
- description: nctId path parameters should match the NCT identifier pattern.
  given: $.paths[?(@property.match(/{nctId}/))]
  name: ctg-nct-id-pattern
  severity: warn
rules_file: rules/clinical-trials-gov-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clinical-trials-gov/refs/heads/main/rules/clinical-trials-gov-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: clinical-trials-gov-rules
source_filename: clinical-trials-gov-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for the ClinicalTrials.gov Data API v2.\n# https://clinicaltrials.gov/data-api/api — open, unauthenticated,\n# JSON-by-default REST API hosted at https://clinicaltrials.gov/api/v2.\nrules:\n  ctg-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  ctg-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  ctg-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  ctg-server-versioned:\n    description: Data API server URL must include /api/v2.\n    severity: warn\n    given: \"$.servers[?(@.url && @.url.indexOf('clinicaltrials.gov')\
  \ > -1)].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/api/v2$\"\n\n  ctg-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  ctg-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  ctg-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  ctg-pagination-page-size:\n    description: List endpoints should support pageSize and pageToken parameters.\n    severity: info\n    given:\
  \ \"$.paths[?(@property == '/studies')].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - pageSize\n          - pageToken\n          - query.term\n          - query.cond\n          - query.intr\n          - query.locn\n          - filter.overallStatus\n          - format\n          - countTotal\n          - fields\n\n  ctg-nct-id-pattern:\n    description: nctId path parameters should match the NCT identifier pattern.\n    severity: warn\n    given: \"$.paths[?(@property.match(/{nctId}/))]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/clinical-trials-gov/refs/heads/main/rules/clinical-trials-gov-rules.yml
tags:
- Clinical Trials
- Government
- Health
- NIH
- Open Data
- Public Health
- Research
- Spectral
- Linting
- API Governance
---
