---
categories:
- csda
description: Spectral linting rules defining API design standards and conventions for Cloud Storage and Data Acquisition.
layout: rules
name: Cloud Storage and Data Acquisition API Rules
provider_name: Cloud Storage and Data Acquisition
provider_slug: cloud-storage-and-data-acquisition
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: csda-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: csda-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: csda-server-https
  severity: error
- description: A security scheme must be defined.
  given: $.components.securitySchemes
  name: csda-security-required
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: csda-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: csda-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: csda-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: csda-error-responses
  severity: warn
- description: List endpoints should support a continuation/page token.
  given: $.paths[?(@property.match(/list$|jobs$|datasets$|buckets$|objects$/))].get.parameters[*].name
  name: csda-pagination-tokens
  severity: info
rules_file: rules/cloud-storage-and-data-acquisition-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloud-storage-and-data-acquisition/refs/heads/main/rules/cloud-storage-and-data-acquisition-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 4
slug: cloud-storage-and-data-acquisition-rules
source_filename: cloud-storage-and-data-acquisition-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for any Cloud Storage / Data Acquisition\n# API in this topic profile. These rules apply to ingestion,\n# transfer, and storage REST APIs and enforce baseline hygiene\n# expected of high-throughput data plane services.\nrules:\n  csda-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  csda-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  csda-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  csda-security-required:\n    description: A security scheme must be defined.\n    severity: error\n    given: \"$.components.securitySchemes\"\
  \n    then:\n      function: truthy\n\n  csda-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  csda-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  csda-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  csda-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function:\
  \ schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n\n  csda-pagination-tokens:\n    description: List endpoints should support a continuation/page token.\n    severity: info\n    given: \"$.paths[?(@property.match(/list$|jobs$|datasets$|buckets$|objects$/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - pageToken\n          - nextToken\n          - continuation-token\n          - marker\n          - cursor\n          - limit\n          - maxResults\n          - prefix\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloud-storage-and-data-acquisition/refs/heads/main/rules/cloud-storage-and-data-acquisition-rules.yml
tags:
- Bulk Transfer
- Change Data Capture
- Cloud Storage
- Data Acquisition
- Data Ingestion
- Data Lake
- ETL
- Object Storage
- Pipelines
- Streaming
- Spectral
- Linting
- API Governance
---
