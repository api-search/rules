---
api_specs:
- filename: service-fabric-cluster-openapi.yml
  format: yaml
  label: Service Fabric Cluster Management API
  slug: service-fabric-cluster-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/service-fabric/refs/heads/main/openapi/service-fabric-cluster-openapi.yml
categories:
- service
description: Spectral linting rules defining API design standards and conventions for Service Fabric.
layout: rules
name: Service Fabric API Rules
provider_name: Service Fabric
provider_slug: service-fabric
rule_count: 8
rules:
- description: Service Fabric operationIds should use camelCase matching the REST style
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: service-fabric-operation-id-pascal-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: service-fabric-operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: service-fabric-operation-summary-required
  severity: error
- description: Service Fabric API requires an api-version query parameter on all operations
  given: $.paths[*][get,post,put,patch,delete]
  name: service-fabric-api-version-required
  severity: warn
- description: Operations must use tags from the defined Service Fabric tag list
  given: $.paths[*][get,post,put,patch,delete].tags[*]
  name: service-fabric-valid-tags
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: service-fabric-tags-required
  severity: error
- description: Health state properties must use standard Service Fabric enum values
  given: $.components.schemas[*].properties[?(@property === 'HealthState' || @property === 'AggregatedHealthState')]
  name: service-fabric-health-state-enum
  severity: info
- description: Operations must define a success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: service-fabric-success-response
  severity: error
rules_file: rules/service-fabric-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/service-fabric/refs/heads/main/rules/service-fabric-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 3
slug: service-fabric-rules
source_filename: service-fabric-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # Service Fabric API uses PascalCase for operationIds\n  service-fabric-operation-id-pascal-case:\n    description: Service Fabric operationIds should use camelCase matching the REST style\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have operationId\n  service-fabric-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  # All operations must have a summary\n  service-fabric-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation must have a summary\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  # Service Fabric always requires api-version parameter\n  service-fabric-api-version-required:\n    description: Service Fabric API requires an api-version query parameter on all operations\n    message: \"Operation should include the api-version query parameter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: parameters\n      function: defined\n\n  # Tags must be from allowed list\n  service-fabric-valid-tags:\n    description: Operations must use tags from the defined Service Fabric tag list\n    message: \"Tag '{{value}}' is not in the Service Fabric tag list\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Cluster\n          - Nodes\n          - Applications\n      \
  \    - Services\n          - Partitions\n          - Health\n\n  # All operations must have tags\n  service-fabric-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  # Health state enum values should be consistent\n  service-fabric-health-state-enum:\n    description: Health state properties must use standard Service Fabric enum values\n    message: \"HealthState enum should include Invalid, Ok, Warning, Error, Unknown\"\n    severity: info\n    given: \"$.components.schemas[*].properties[?(@property === 'HealthState' || @property === 'AggregatedHealthState')]\"\n    then:\n      function: defined\n\n  # Responses should define success codes\n  service-fabric-success-response:\n    description: Operations must define a success response\n\
  \    message: \"Operation must have a 200 or 201 response defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/service-fabric/refs/heads/main/rules/service-fabric-rules.yml
tags:
- Distributed Systems
- Microservices
- Containers
- Cloud Native
- Kubernetes
- Azure
- Open Source
- Spectral
- Linting
- API Governance
---
