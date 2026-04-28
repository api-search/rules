---
categories:
- clickhouse
description: Spectral linting rules defining API design standards and conventions for ClickHouse.
layout: rules
name: ClickHouse API Rules
provider_name: ClickHouse
provider_slug: clickhouse
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: clickhouse-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clickhouse-info-license
  severity: warn
- description: All server URLs must use HTTPS for the Cloud control plane.
  given: $.servers[?(@.url && @.url.indexOf('clickhouse.cloud') > -1)].url
  name: clickhouse-server-https
  severity: error
- description: ClickHouse Cloud paths must be versioned (/v{N}).
  given: $.paths
  name: clickhouse-cloud-versioned
  severity: warn
- description: A security scheme (apiKey) must be declared for Cloud APIs.
  given: $.components.securitySchemes
  name: clickhouse-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickhouse-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickhouse-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clickhouse-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clickhouse-error-responses
  severity: warn
rules_file: rules/clickhouse-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clickhouse/refs/heads/main/rules/clickhouse-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: clickhouse-rules
tags:
- Analytics
- Cloud Database
- Column-Oriented
- Database
- OLAP
- Open Source
- Real-Time
- SQL
- Spectral
- Linting
- API Governance
---
