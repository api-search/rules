---
api_specs:
- filename: vmware-tanzu-service-mesh-openapi.yml
  format: yaml
  label: VMware Tanzu Service Mesh API
  slug: tanzu-service-mesh-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vmware-tanzu/refs/heads/main/openapi/vmware-tanzu-service-mesh-openapi.yml
- filename: vmware-tanzu-kubernetes-grid-openapi.yml
  format: yaml
  label: VMware Tanzu Kubernetes Grid API
  slug: tanzu-kubernetes-grid-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vmware-tanzu/refs/heads/main/openapi/vmware-tanzu-kubernetes-grid-openapi.yml
categories:
- tanzu
description: Spectral linting rules defining API design standards and conventions for VMware Tanzu.
layout: rules
name: VMware Tanzu API Rules
provider_name: VMware Tanzu
provider_slug: vmware-tanzu
rule_count: 8
rules:
- description: Operation IDs must use camelCase to match Tanzu SDK conventions.
  given: $.paths[*][*].operationId
  name: tanzu-operation-ids-camel-case
  severity: warn
- description: All Tanzu API operations must define security.
  given: $.paths[*][*]
  name: tanzu-require-auth
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][*]
  name: tanzu-require-summaries
  severity: error
- description: All operations and schemas must have descriptions.
  given:
  - $.paths[*][*]
  - $.components.schemas[*]
  name: tanzu-require-descriptions
  severity: warn
- description: All authenticated operations must define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete]
  name: tanzu-require-401-response
  severity: warn
- description: All path parameters must have descriptions.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: tanzu-path-params-documented
  severity: warn
- description: All Tanzu API paths must include an API version segment.
  given: $.paths
  name: tanzu-versioned-paths
  severity: warn
- description: All schema properties must have explicit types.
  given: $.components.schemas[*].properties[*]
  name: tanzu-schemas-have-types
  severity: warn
rules_file: rules/vmware-tanzu-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vmware-tanzu/refs/heads/main/rules/vmware-tanzu-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: vmware-tanzu-rules
source_filename: vmware-tanzu-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  tanzu-operation-ids-camel-case:\n    description: Operation IDs must use camelCase to match Tanzu SDK conventions.\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tanzu-require-auth:\n    description: All Tanzu API operations must define security.\n    message: \"Operation {{path}} must define security\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  tanzu-require-summaries:\n    description: All operations must have a summary.\n    message: \"Operation {{path}} must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  tanzu-require-descriptions:\n    description: All operations and schemas must have descriptions.\n    message:\
  \ \"{{path}} must have a description\"\n    severity: warn\n    given:\n      - \"$.paths[*][*]\"\n      - \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  tanzu-require-401-response:\n    description: All authenticated operations must define a 401 Unauthorized response.\n    message: \"Operation {{path}} must define a 401 response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  tanzu-path-params-documented:\n    description: All path parameters must have descriptions.\n    message: \"Path parameter {{path}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: description\n      function: truthy\n\n  tanzu-versioned-paths:\n    description: All Tanzu API paths must include an API version segment.\n    message: \"Path {{path}} should include a version segment (v1alpha1, v1alpha2,\
  \ etc.)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(v[0-9]|apis|csp)/\"\n\n  tanzu-schemas-have-types:\n    description: All schema properties must have explicit types.\n    message: \"Schema property {{path}} must have a type\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: type\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vmware-tanzu/refs/heads/main/rules/vmware-tanzu-rules.yml
tags:
- Cloud Native
- Containers
- Enterprise
- Kubernetes
- Multi-Cloud
- Service Mesh
- VMware
- Spectral
- Linting
- API Governance
---
