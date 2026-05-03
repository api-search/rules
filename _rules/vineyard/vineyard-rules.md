---
api_specs:
- filename: vineyard-python-client-openapi.yml
  format: yaml
  label: Vineyard Python Client API
  slug: vineyard-python-client
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vineyard/refs/heads/main/openapi/vineyard-python-client-openapi.yml
categories:
- vineyard
description: Spectral linting rules defining API design standards and conventions for Vineyard.
layout: rules
name: Vineyard API Rules
provider_name: Vineyard
provider_slug: vineyard
rule_count: 8
rules:
- description: Operation IDs should use camelCase consistent with vineyard Python SDK naming
  given: $.paths[*][*].operationId
  name: vineyard-operation-ids-kebab-case
  severity: warn
- description: All operations must have at least one tag for grouping
  given: $.paths[*][*]
  name: vineyard-tags-required
  severity: error
- description: All path segments should use kebab-case
  given: $.paths
  name: vineyard-path-kebab-case
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: vineyard-description-required
  severity: error
- description: Successful operations should return 200 or 201
  given: $.paths[*][post,put,patch]
  name: vineyard-response-200-or-201
  severity: warn
- description: ObjectIDs in vineyard are 64-bit unsigned integers represented as strings for JSON compatibility
  given: $.paths[*][*].parameters[?(@.name == 'objectId')]
  name: vineyard-object-id-string
  severity: warn
- description: At least one server must be defined in the spec
  given: $
  name: vineyard-server-defined
  severity: error
- description: The info object should include contact information
  given: $.info
  name: vineyard-info-contact
  severity: warn
rules_file: rules/vineyard-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vineyard/refs/heads/main/rules/vineyard-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 5
slug: vineyard-rules
source_filename: vineyard-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vineyard-operation-ids-kebab-case:\n    description: Operation IDs should use camelCase consistent with vineyard Python SDK naming\n    message: \"Operation ID '{{value}}' should be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  vineyard-tags-required:\n    description: All operations must have at least one tag for grouping\n    message: \"Operation is missing tags - use Connection, Objects, Metadata, Names, Blobs, or Persistence\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  vineyard-path-kebab-case:\n    description: All path segments should use kebab-case\n    message: \"Path '{{path}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}/]+)+$\"\
  \n\n  vineyard-description-required:\n    description: All operations must have a description\n    message: \"Operation at '{{path}}' is missing a description\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  vineyard-response-200-or-201:\n    description: Successful operations should return 200 or 201\n    message: \"Operation should define a 200 or 201 success response\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          oneOf:\n            - required: ['200']\n            - required: ['201']\n\n  vineyard-object-id-string:\n    description: >-\n      ObjectIDs in vineyard are 64-bit unsigned integers represented as strings\n      for JSON compatibility\n    message: \"ObjectID path parameter should be type string\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name == 'objectId')]\"\
  \n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  vineyard-server-defined:\n    description: At least one server must be defined in the spec\n    message: \"The spec should define at least one server\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  vineyard-info-contact:\n    description: The info object should include contact information\n    message: \"info.contact should be defined for community support\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vineyard/refs/heads/main/rules/vineyard-rules.yml
tags:
- Big Data
- CNCF
- Cloud Native
- Data Engineering
- Distributed Systems
- In-Memory Storage
- Kubernetes
- Machine Learning
- Metadata Management
- Python
- Zero-Copy
- Spectral
- Linting
- API Governance
---
