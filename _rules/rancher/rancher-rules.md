---
api_specs:
- filename: rancher-management-api-openapi.yml
  format: yaml
  label: Rancher Management API
  slug: rancher-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rancher/refs/heads/main/openapi/rancher-management-api-openapi.yml
categories:
- rancher
description: Spectral linting rules defining API design standards and conventions for Rancher.
layout: rules
name: Rancher API Rules
provider_name: Rancher
provider_slug: rancher
rule_count: 7
rules:
- description: All operationIds must use camelCase to match the Rancher Management API convention.
  given: $.paths[*][*].operationId
  name: rancher-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: rancher-tags-title-case
  severity: warn
- description: All operations should use BearerAuth security scheme.
  given: $.paths[*][*]
  name: rancher-bearer-auth-required
  severity: warn
- description: Collection GET endpoints should return a typed collection with 'data' array.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: rancher-collection-responses
  severity: hint
- description: Resource identifier path parameters should be named 'id'.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: rancher-resource-ids-path-params
  severity: hint
- description: DELETE operations should return 204 No Content.
  given: $.paths[*].delete.responses
  name: rancher-delete-returns-204
  severity: warn
- description: API paths must not end with a trailing slash.
  given: $.paths
  name: rancher-no-trailing-slashes
  severity: error
rules_file: rules/rancher-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rancher/refs/heads/main/rules/rancher-rules.yml
severity_counts:
  error: 1
  hint: 2
  info: 0
  warn: 4
slug: rancher-rules
source_filename: rancher-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rancher-operation-ids-camel-case:\n    description: All operationIds must use camelCase to match the Rancher Management API convention.\n    message: \"OperationId '{{value}}' must be camelCase (e.g., listClusters, createCluster).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rancher-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]*$\"\n\n  rancher-bearer-auth-required:\n    description: All operations should use BearerAuth security scheme.\n    message: \"Operation at '{{path}}' should specify BearerAuth security.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n\
  \      function: truthy\n\n  rancher-collection-responses:\n    description: Collection GET endpoints should return a typed collection with 'data' array.\n    message: \"Collection endpoint should return an object with 'data' array following Rancher's collection pattern.\"\n    severity: hint\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n\n  rancher-resource-ids-path-params:\n    description: Resource identifier path parameters should be named 'id'.\n    message: \"Path parameter for resource identifier should be named 'id'.\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: truthy\n\n  rancher-delete-returns-204:\n    description: DELETE operations should return 204 No Content.\n    message: \"DELETE operation at '{{path}}' should define a 204 response.\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field:\
  \ 204\n      function: truthy\n\n  rancher-no-trailing-slashes:\n    description: API paths must not end with a trailing slash.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rancher/refs/heads/main/rules/rancher-rules.yml
tags:
- Cluster Management
- Containers
- Kubernetes
- Multi-Cluster
- Open Source
- SUSE
- Platform Engineering
- Spectral
- Linting
- API Governance
---
