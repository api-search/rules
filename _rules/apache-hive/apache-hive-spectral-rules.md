---
categories:
- hive
description: Spectral linting rules defining API design standards and conventions for Apache Hive.
layout: rules
name: Apache Hive API Rules
provider_name: Apache Hive
provider_slug: apache-hive
rule_count: 8
rules:
- description: All Hive WebHCat API operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: hive-operation-summary
  severity: error
- description: All Hive WebHCat API operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: hive-operation-id
  severity: error
- description: All Hive WebHCat API operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: hive-operation-tags
  severity: warn
- description: All Hive schema components must have a description
  given: $.components.schemas[*]
  name: hive-schema-description
  severity: warn
- description: All Hive schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: hive-property-description
  severity: info
- description: API info must include contact information
  given: $.info
  name: hive-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: hive-info-license
  severity: warn
- description: All Hive path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: hive-path-parameters-described
  severity: warn
rules_file: rules/apache-hive-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-hive/refs/heads/main/rules/apache-hive-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: apache-hive-spectral-rules
tags:
- Apache
- Big Data
- Data Warehouse
- ETL
- Hadoop
- Open Source
- SQL
- Spectral
- Linting
- API Governance
---
