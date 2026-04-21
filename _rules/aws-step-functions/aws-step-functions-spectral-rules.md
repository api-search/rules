---
categories:
- sfn
description: Spectral linting rules defining API design standards and conventions for AWS Step Functions.
layout: rules
name: AWS Step Functions API Rules
provider_name: AWS Step Functions
provider_slug: aws-step-functions
rule_count: 8
rules:
- description: All operations must have a summary starting with "AWS Step Functions"
  given: $.paths[*][get,post,put,delete,patch]
  name: sfn-operation-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: sfn-operation-id
  severity: error
- description: Info object must have a title
  given: $.info
  name: sfn-info-title
  severity: error
- description: Info object must have a version
  given: $.info
  name: sfn-info-version
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: sfn-response-description
  severity: error
- description: Operations should have x-microcks-operation annotation
  given: $.paths[*][get,post,put,delete,patch]
  name: sfn-microcks-annotation
  severity: info
- description: Schema components should have a type
  given: $.components.schemas[*]
  name: sfn-schema-type
  severity: warn
- description: API security schemes should be defined
  given: $
  name: sfn-security-defined
  severity: warn
rules_file: rules/aws-step-functions-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-step-functions/refs/heads/main/rules/aws-step-functions-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 3
slug: aws-step-functions-spectral-rules
tags:
- AWS
- iPaaS
- Orchestration
- Serverless
- Spectral
- Linting
- API Governance
---
