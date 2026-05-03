---
api_specs:
- filename: red-hat-openshift-api-openapi.yml
  format: yaml
  label: Red Hat OpenShift Container Platform API
  slug: openshift-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-openshift/refs/heads/main/openapi/red-hat-openshift-api-openapi.yml
- filename: openapi
  format: yaml
  label: Red Hat OpenShift Cluster Manager API
  slug: openshift-cluster-manager-api
  spec_type: OpenAPI
  url: https://api.openshift.com/openapi
categories:
- openshift
description: Spectral linting rules defining API design standards and conventions for Red Hat OpenShift.
layout: rules
name: Red Hat OpenShift API Rules
provider_name: Red Hat OpenShift
provider_slug: red-hat-openshift
rule_count: 13
rules:
- description: All OpenShift resource schemas must include apiVersion and kind fields to follow the Kubernetes object model conventions.
  given: $.components.schemas[*].properties
  name: openshift-api-version-required
  severity: error
- description: OpenShift API requires Bearer token authentication. Security schemes must define bearerAuth using HTTP bearer scheme.
  given: $.components.securitySchemes.bearerAuth
  name: openshift-bearer-auth
  severity: error
- description: All OpenShift API operations must have an operationId for SDK generation, client library support, and documentation.
  given: $.paths[*][get,post,put,delete,patch]
  name: openshift-operation-id-required
  severity: error
- description: 'All path template parameters (e.g., {namespace}, {name}) must be defined in the parameters array with required: true.'
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in === 'path')]
  name: openshift-path-params-defined
  severity: error
- description: The namespace path parameter must be of type string in all namespaced OpenShift resource paths.
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'namespace')].schema
  name: openshift-namespace-param-type
  severity: warn
- description: The name path parameter must be of type string in all OpenShift resource paths following Kubernetes naming conventions.
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'name')].schema
  name: openshift-name-param-string
  severity: warn
- description: List operations should support the labelSelector query parameter for filtering resources by labels, following Kubernetes conventions.
  given: $.paths[*][get]
  name: openshift-list-label-selector
  severity: info
- description: List response schemas must include an items array to hold the collection of returned resources.
  given: $.components.schemas[?@property.endsWith('List')].properties
  name: openshift-list-response-items
  severity: error
- description: OpenShift resource schemas should reference ObjectMeta for consistent metadata handling across resource types.
  given: $.components.schemas[*].properties
  name: openshift-object-meta-used
  severity: info
- description: All operations must include a description explaining the resource type, available parameters, and expected behavior.
  given: $.paths[*][get,post,put,delete,patch]
  name: openshift-operation-description
  severity: warn
- description: All OpenShift API paths must include version segments following the /apis/{group}/{version}/ pattern.
  given: $.paths[*~]
  name: openshift-api-versioned-paths
  severity: error
- description: OpenShift API servers must use HTTPS and include the standard port 6443 for API server communication.
  given: $.servers[*]
  name: openshift-server-url
  severity: info
- description: All protected OpenShift API endpoints must define a 401 Unauthorized response for unauthenticated access attempts.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: openshift-401-response
  severity: warn
rules_file: rules/red-hat-openshift-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/red-hat-openshift/refs/heads/main/rules/red-hat-openshift-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 3
  warn: 4
slug: red-hat-openshift-rules
source_filename: red-hat-openshift-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # OpenShift resources must include apiVersion and kind\n  openshift-api-version-required:\n    description: >-\n      All OpenShift resource schemas must include apiVersion and kind fields\n      to follow the Kubernetes object model conventions.\n    severity: error\n    given: $.components.schemas[*].properties\n    then:\n      field: apiVersion\n      function: defined\n\n  # Bearer token authentication required\n  openshift-bearer-auth:\n    description: >-\n      OpenShift API requires Bearer token authentication. Security schemes\n      must define bearerAuth using HTTP bearer scheme.\n    severity: error\n    given: $.components.securitySchemes.bearerAuth\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: \"^bearer$\"\n\n  # Operations require operation IDs\n  openshift-operation-id-required:\n    description: >-\n      All OpenShift API operations must have an operationId for SDK\n     \
  \ generation, client library support, and documentation.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  # Path parameters must be defined in parameters\n  openshift-path-params-defined:\n    description: >-\n      All path template parameters (e.g., {namespace}, {name}) must be\n      defined in the parameters array with required: true.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.in === 'path')]\n    then:\n      field: required\n      function: pattern\n      functionOptions:\n        match: \"^true$\"\n\n  # Namespace parameter type\n  openshift-namespace-param-type:\n    description: >-\n      The namespace path parameter must be of type string in all\n      namespaced OpenShift resource paths.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'namespace')].schema\n    then:\n      field: type\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^string$\"\n\n  # Name parameter type\n  openshift-name-param-string:\n    description: >-\n      The name path parameter must be of type string in all OpenShift\n      resource paths following Kubernetes naming conventions.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name === 'name')].schema\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\n  # List operations should support labelSelector\n  openshift-list-label-selector:\n    description: >-\n      List operations should support the labelSelector query parameter\n      for filtering resources by labels, following Kubernetes conventions.\n    severity: info\n    given: $.paths[*][get]\n    then:\n      function: truthy\n\n  # Response schemas for resource lists\n  openshift-list-response-items:\n    description: >-\n      List response schemas must include an items array to hold the\
  \ collection\n      of returned resources.\n    severity: error\n    given: $.components.schemas[?@property.endsWith('List')].properties\n    then:\n      field: items\n      function: truthy\n\n  # ObjectMeta should be referenced\n  openshift-object-meta-used:\n    description: >-\n      OpenShift resource schemas should reference ObjectMeta for consistent\n      metadata handling across resource types.\n    severity: info\n    given: $.components.schemas[*].properties\n    then:\n      field: metadata\n      function: defined\n\n  # Operations must have descriptions\n  openshift-operation-description:\n    description: >-\n      All operations must include a description explaining the resource\n      type, available parameters, and expected behavior.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  # API versions should use /v1 or versioned format\n  openshift-api-versioned-paths:\n    description:\
  \ >-\n      All OpenShift API paths must include version segments following\n      the /apis/{group}/{version}/ pattern.\n    severity: error\n    given: $.paths[*~]\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api(s)?(/[a-z][a-z0-9.-]*)?/v[0-9]+\"\n\n  # Server URL format\n  openshift-server-url:\n    description: >-\n      OpenShift API servers must use HTTPS and include the standard port 6443\n      for API server communication.\n    severity: info\n    given: $.servers[*]\n    then:\n      field: url\n      function: truthy\n\n  # 401 responses for all protected endpoints\n  openshift-401-response:\n    description: >-\n      All protected OpenShift API endpoints must define a 401 Unauthorized\n      response for unauthenticated access attempts.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].responses\n    then:\n      field: '401'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red-hat-openshift/refs/heads/main/rules/red-hat-openshift-rules.yml
tags:
- Containers
- Enterprise
- Hybrid Cloud
- Kubernetes
- PaaS
- Red Hat
- Spectral
- Linting
- API Governance
---
