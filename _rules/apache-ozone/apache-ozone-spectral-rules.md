---
categories:
- info
- operation
- paths
- security
description: Spectral linting rules defining API design standards and conventions for Apache Ozone.
layout: rules
name: Apache Ozone API Rules
provider_name: Apache Ozone
provider_slug: apache-ozone
rule_count: 6
rules:
- description: API must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: Summaries should start with Apache Ozone
  given: $.paths[*][get,post,put,delete,patch,head].summary
  name: operation-summary-apache-prefix
  severity: info
- description: Paths should follow S3 bucket/key pattern
  given: $.paths[*]~
  name: paths-s3-compatible
  severity: info
- description: S3 API should use AWS Signature authentication
  given: $.info
  name: security-s3-auth
  severity: warn
rules_file: rules/apache-ozone-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-ozone/refs/heads/main/rules/apache-ozone-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 1
slug: apache-ozone-spectral-rules
tags:
- Distributed Storage
- Hadoop
- Object Storage
- S3-Compatible
- Apache
- Open Source
- Spectral
- Linting
- API Governance
---
