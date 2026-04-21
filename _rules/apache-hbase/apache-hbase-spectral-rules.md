---
categories:
- hbase
description: Spectral linting rules defining API design standards and conventions for Apache HBase.
layout: rules
name: Apache HBase API Rules
provider_name: Apache HBase
provider_slug: apache-hbase
rule_count: 9
rules:
- description: All HBase REST API operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: hbase-operation-summary
  severity: error
- description: All HBase REST API operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: hbase-operation-id
  severity: error
- description: All HBase REST API operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: hbase-operation-tags
  severity: warn
- description: All HBase schema components must have a description
  given: $.components.schemas[*]
  name: hbase-schema-description
  severity: warn
- description: All HBase schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: hbase-property-description
  severity: info
- description: API info must include contact information
  given: $.info
  name: hbase-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: hbase-info-license
  severity: warn
- description: All HBase path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: hbase-path-parameters-described
  severity: warn
- description: All HBase operations must define at least one 2xx response
  given: $.paths[*][get,put,post,delete,patch].responses
  name: hbase-success-response
  severity: error
rules_file: rules/apache-hbase-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-hbase/refs/heads/main/rules/apache-hbase-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: apache-hbase-spectral-rules
tags:
- Apache
- Big Data
- Bigtable
- Database
- Hadoop
- NoSQL
- Open Source
- Wide Column
- Spectral
- Linting
- API Governance
---
