---
categories:
- s3
description: Spectral linting rules defining API design standards and conventions for Amazon S3 API.
layout: rules
name: Amazon S3 API API Rules
provider_name: Amazon S3 API
provider_slug: aws-s3
rule_count: 10
rules:
- description: All operations must have a summary starting with "Amazon S3"
  given: $.paths[*][get,post,put,delete,patch,head]
  name: s3-operation-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch,head]
  name: s3-operation-id
  severity: error
- description: Info object must have a title
  given: $.info
  name: s3-info-title
  severity: error
- description: Info object must have a version
  given: $.info
  name: s3-info-version
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: s3-response-description
  severity: error
- description: All parameters should have a description
  given: $.paths[*][*].parameters[*]
  name: s3-parameter-description
  severity: warn
- description: Operations should have x-microcks-operation annotation
  given: $.paths[*][get,post,put,delete,patch,head]
  name: s3-microcks-annotation
  severity: info
- description: Schema components should have a type
  given: $.components.schemas[*]
  name: s3-schema-type
  severity: warn
- description: API security schemes should be defined
  given: $
  name: s3-security-defined
  severity: warn
- description: Servers array should be defined
  given: $
  name: s3-servers-defined
  severity: warn
rules_file: rules/aws-s3-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-s3/refs/heads/main/rules/aws-s3-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: aws-s3-spectral-rules
tags:
- AWS
- Cloud Storage
- Object Storage
- Storage
- Spectral
- Linting
- API Governance
---
