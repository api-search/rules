---
categories:
- helix
description: Spectral linting rules defining API design standards and conventions for Apache Helix.
layout: rules
name: Apache Helix API Rules
provider_name: Apache Helix
provider_slug: apache-helix
rule_count: 8
rules:
- description: All Helix REST API operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: helix-operation-summary
  severity: error
- description: All Helix REST API operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: helix-operation-id
  severity: error
- description: All Helix REST API operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: helix-operation-tags
  severity: warn
- description: All Helix schema components must have a description
  given: $.components.schemas[*]
  name: helix-schema-description
  severity: warn
- description: All Helix schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: helix-property-description
  severity: info
- description: API info must include contact information
  given: $.info
  name: helix-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: helix-info-license
  severity: warn
- description: All Helix path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: helix-path-parameters-described
  severity: warn
rules_file: rules/apache-helix-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-helix/refs/heads/main/rules/apache-helix-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: apache-helix-spectral-rules
tags:
- Apache
- Cluster Management
- Distributed Systems
- Open Source
- Partitioning
- Replication
- Spectral
- Linting
- API Governance
---
