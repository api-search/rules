---
categories:
- redshift
description: Spectral linting rules defining API design standards and conventions for AWS Redshift.
layout: rules
name: AWS Redshift API Rules
provider_name: AWS Redshift
provider_slug: aws-redshift
rule_count: 11
rules:
- description: All operations must have a summary starting with "Amazon Redshift"
  given: $.paths[*][get,post,put,delete,patch]
  name: redshift-operation-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: redshift-operation-id
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: redshift-operation-description
  severity: warn
- description: Components schemas should be defined
  given: $.components
  name: redshift-components-schemas
  severity: warn
- description: API security schemes should be defined
  given: $
  name: redshift-security-defined
  severity: warn
- description: Info object must have a title
  given: $.info
  name: redshift-info-title
  severity: error
- description: Info object must have a version
  given: $.info
  name: redshift-info-version
  severity: error
- description: All parameters should have a description
  given: $.paths[*][*].parameters[*]
  name: redshift-parameter-description
  severity: warn
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: redshift-response-description
  severity: error
- description: Schema properties should have a type
  given: $.components.schemas[*]
  name: redshift-schema-type
  severity: warn
- description: Operations should have x-microcks-operation annotation
  given: $.paths[*][get,post,put,delete,patch]
  name: redshift-microcks-annotation
  severity: info
rules_file: rules/aws-redshift-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-redshift/refs/heads/main/rules/aws-redshift-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 6
slug: aws-redshift-spectral-rules
tags:
- Analytics
- Big Data
- Cloud Database
- Data Warehouse
- SQL
- Spectral
- Linting
- API Governance
---
