---
categories:
- cockroach
description: Spectral linting rules defining API design standards and conventions for Cockroach Labs.
layout: rules
name: Cockroach Labs API Rules
provider_name: Cockroach Labs
provider_slug: cockroach-labs
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: cockroach-labs-info-contact
  severity: error
- description: termsOfService must reference cockroachlabs.com.
  given: $.info.termsOfService
  name: cockroach-labs-terms-of-service
  severity: warn
- description: Public server URLs must use HTTPS (cluster API loopback exempt).
  given: $.servers[?(@.url && @.url.indexOf('localhost') === -1)].url
  name: cockroach-labs-server-https
  severity: warn
- description: Cloud API server URL must point to cockroachlabs.cloud.
  given: $.servers[?(@.url && @.url.indexOf('cockroachlabs.cloud') > -1)].url
  name: cockroach-labs-cloud-base-host
  severity: info
- description: Cloud API operations must define a bearer-token security scheme.
  given: $.components.securitySchemes[*]
  name: cockroach-labs-bearer-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cockroach-labs-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cockroach-labs-operation-tags
  severity: warn
- description: Mutating operations should declare 4xx/5xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cockroach-labs-error-responses
  severity: warn
- description: Path parameters named cluster_id should be UUIDs.
  given: $.paths[*].*.parameters[?(@.in == 'path' && @.name == 'cluster_id')].schema
  name: cockroach-labs-uuid-cluster-id
  severity: info
- description: Cloud API requests should support the Cc-Version versioning header.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'header')]
  name: cockroach-labs-cc-version-header
  severity: info
rules_file: rules/cockroach-labs-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cockroach-labs/refs/heads/main/rules/cockroach-labs-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 3
  warn: 4
slug: cockroach-labs-rules
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
