---
categories:
- xray
description: Spectral linting rules defining API design standards and conventions for AWS X-Ray.
layout: rules
name: AWS X-Ray API Rules
provider_name: AWS X-Ray
provider_slug: aws-x-ray
rule_count: 5
rules:
- description: All operations must have a summary starting with "AWS X-Ray"
  given: $.paths[*][get,post,put,delete,patch]
  name: xray-operation-summary
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: xray-operation-id
  severity: error
- description: Info object must have a title
  given: $.info
  name: xray-info-title
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: xray-response-description
  severity: error
- description: Operations should have x-microcks-operation annotation
  given: $.paths[*][get,post,put,delete,patch]
  name: xray-microcks-annotation
  severity: info
rules_file: rules/aws-x-ray-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-x-ray/refs/heads/main/rules/aws-x-ray-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 1
slug: aws-x-ray-spectral-rules
tags:
- AWS
- Debugging
- Distributed Tracing
- Microservices
- Observability
- Spectral
- Linting
- API Governance
---
