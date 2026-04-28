---
categories:
- cockroachdb
description: Spectral linting rules defining API design standards and conventions for CockroachDB.
layout: rules
name: CockroachDB API Rules
provider_name: CockroachDB
provider_slug: cockroachdb
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: cockroachdb-info-contact
  severity: error
- description: termsOfService must reference cockroachlabs.com.
  given: $.info.termsOfService
  name: cockroachdb-terms-of-service
  severity: warn
- description: Public server URLs must use HTTPS (cluster API loopback exempt).
  given: $.servers[?(@.url && @.url.indexOf('localhost') === -1)].url
  name: cockroachdb-server-https
  severity: warn
- description: Cloud API server URL must point to cockroachlabs.cloud.
  given: $.servers[?(@.url && @.url.indexOf('cockroachlabs.cloud') > -1)].url
  name: cockroachdb-cloud-base-host
  severity: info
- description: Cloud API operations must define a bearer-token security scheme.
  given: $.components.securitySchemes[*]
  name: cockroachdb-bearer-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cockroachdb-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cockroachdb-operation-tags
  severity: warn
- description: Mutating operations should declare 4xx/5xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cockroachdb-error-responses
  severity: warn
- description: Path parameters named cluster_id should be UUIDs.
  given: $.paths[*].*.parameters[?(@.in == 'path' && @.name == 'cluster_id')].schema
  name: cockroachdb-uuid-cluster-id
  severity: info
- description: Use canonical CockroachDB request headers (Cc-Version, X-Cockroach-API-Session, Authorization).
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'header')]
  name: cockroachdb-headers-allowlist
  severity: info
rules_file: rules/cockroachdb-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cockroachdb/refs/heads/main/rules/cockroachdb-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 3
  warn: 4
slug: cockroachdb-rules
tags:
- Cluster Management
- Cloud
- Database
- Distributed SQL
- Infrastructure
- PostgreSQL Compatible
- SQL
- Spectral
- Linting
- API Governance
---
