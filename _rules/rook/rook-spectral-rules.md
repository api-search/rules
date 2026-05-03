---
api_specs:
- filename: rook-ceph-object-storage-openapi.yml
  format: yaml
  label: Rook Ceph Object Storage API
  slug: rook-ceph-object-storage-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rook/refs/heads/main/openapi/rook-ceph-object-storage-openapi.yml
categories:
- rook
description: Spectral linting rules defining API design standards and conventions for Rook.
layout: rules
name: Rook API Rules
provider_name: Rook
provider_slug: rook
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: rook-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: rook-operation-id-camel-case
  severity: warn
- description: S3 paths with /{key} must also include /{bucket} parameter
  given: $.paths[*][get,put,delete,head].parameters[?(@.in == 'path')]
  name: rook-s3-path-bucket-required
  severity: error
- description: S3-compatible responses should use application/xml content type
  given: $.paths[*][*].responses[*].content
  name: rook-s3-response-xml-content-type
  severity: info
- description: All operations must have a description
  given: $.paths[*][get,put,post,delete,head]
  name: rook-operation-description-required
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: rook-tags-title-case
  severity: warn
- description: Error responses should reference an ErrorResponse schema
  given: $.paths[*][*].responses[4xx,5xx]
  name: rook-error-response-schema
  severity: info
- description: At least one server must be defined
  given: $
  name: rook-server-defined
  severity: error
- description: Info object must include contact information
  given: $.info
  name: rook-info-contact
  severity: warn
rules_file: rules/rook-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rook/refs/heads/main/rules/rook-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: rook-spectral-rules
source_filename: rook-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Rook S3-compatible API conventions\n  rook-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][^a-z]*([A-Z][^A-Z]*)*$|^([A-Z][a-z]*(\\\\s[A-Z]?[a-z]*)*[A-Z]?[a-z]*)$\"\n\n  rook-operation-id-camel-case:\n    description: operationId must use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rook-s3-path-bucket-required:\n    description: S3 paths with /{key} must also include /{bucket} parameter\n    message: \"S3 path operations on objects must define the 'bucket' path parameter\"\n    severity: error\n  \
  \  given: \"$.paths[*][get,put,delete,head].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: enumeration\n      functionOptions:\n        values:\n          - bucket\n          - key\n\n  rook-s3-response-xml-content-type:\n    description: S3-compatible responses should use application/xml content type\n    message: \"S3 object storage responses should declare application/xml or application/octet-stream content types\"\n    severity: info\n    given: \"$.paths[*][*].responses[*].content\"\n    then:\n      function: truthy\n\n  rook-operation-description-required:\n    description: All operations must have a description\n    message: \"Operation is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,head]\"\n    then:\n      field: description\n      function: truthy\n\n  rook-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given:\
  \ \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  rook-error-response-schema:\n    description: Error responses should reference an ErrorResponse schema\n    message: \"4xx and 5xx responses should include an error response schema\"\n    severity: info\n    given: \"$.paths[*][*].responses[4xx,5xx]\"\n    then:\n      field: content\n      function: truthy\n\n  rook-server-defined:\n    description: At least one server must be defined\n    message: \"OpenAPI spec must define at least one server\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  rook-info-contact:\n    description: Info object must include contact information\n    message: \"OpenAPI info must include a contact block\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rook/refs/heads/main/rules/rook-spectral-rules.yml
tags:
- Block Storage
- CNCF
- Ceph
- Cloud Native
- File Storage
- Graduated
- Kubernetes
- Object Storage
- Orchestration
- Storage
- Spectral
- Linting
- API Governance
---
