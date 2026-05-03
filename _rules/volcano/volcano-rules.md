---
api_specs:
- filename: volcano-job-openapi.yml
  format: yaml
  label: Volcano Batch Scheduling API
  slug: volcano-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/volcano/refs/heads/main/openapi/volcano-job-openapi.yml
- filename: volcano-queue-openapi.yml
  format: yaml
  label: Volcano Queue API
  slug: volcano-queue-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/volcano/refs/heads/main/openapi/volcano-queue-openapi.yml
- filename: volcano-podgroup-openapi.yml
  format: yaml
  label: Volcano PodGroup API
  slug: volcano-podgroup-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/volcano/refs/heads/main/openapi/volcano-podgroup-openapi.yml
categories:
- volcano
description: Spectral linting rules defining API design standards and conventions for Volcano.
layout: rules
name: Volcano API Rules
provider_name: Volcano
provider_slug: volcano
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: volcano-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: volcano-operation-ids-camel-case
  severity: warn
- description: Each operation must have at least one tag.
  given: $.paths[*][*]
  name: volcano-tags-required
  severity: error
- description: Paths must include a Kubernetes API group (e.g. batch.volcano.sh or scheduling.volcano.sh).
  given: $.paths
  name: volcano-kubernetes-api-group-in-path
  severity: warn
- description: Server URL must use a variable for the kubernetes-api-server address.
  given: $.servers[*].url
  name: volcano-server-variable-required
  severity: info
- description: Namespaced resource paths must include a namespace parameter.
  given: $.paths[*namespaces*][get,post,put,patch,delete].parameters[*]
  name: volcano-namespace-path-param
  severity: warn
- description: List operations should support limit and continue query parameters.
  given: $.paths[*][get][operationId][?(@.match(/^list/))]
  name: volcano-list-pagination-support
  severity: info
rules_file: rules/volcano-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/volcano/refs/heads/main/rules/volcano-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 2
  warn: 4
slug: volcano-rules
source_filename: volcano-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  volcano-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*)\"\n\n  volcano-operation-ids-camel-case:\n    description: OperationIds must use camelCase.\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  volcano-tags-required:\n    description: Each operation must have at least one tag.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  volcano-kubernetes-api-group-in-path:\n    description: Paths must include a Kubernetes API group (e.g. batch.volcano.sh or scheduling.volcano.sh).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \".*volcano\\\\.sh.*\"\n\n  volcano-server-variable-required:\n    description: Server URL must use a variable for the kubernetes-api-server address.\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{.*\\\\}.*\"\n\n  volcano-namespace-path-param:\n    description: Namespaced resource paths must include a namespace parameter.\n    severity: warn\n    given: \"$.paths[*namespaces*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - namespace\n          - name\n          - labelSelector\n          - fieldSelector\n          - limit\n          - continue\n\n  volcano-list-pagination-support:\n    description: List operations should support limit and continue query parameters.\n    severity: info\n    given: \"$.paths[*][get][operationId][?(@.match(/^list/))]\"\n\
  \    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/volcano/refs/heads/main/rules/volcano-rules.yml
tags:
- Batch Processing
- Cloud Native
- HPC
- Incubating
- Kubernetes
- Scheduling
- Machine Learning
- Spectral
- Linting
- API Governance
---
