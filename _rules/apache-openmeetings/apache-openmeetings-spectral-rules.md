---
categories:
- info
- operation
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apache OpenMeetings.
layout: rules
name: Apache OpenMeetings API Rules
provider_name: Apache OpenMeetings
provider_slug: apache-openmeetings
rule_count: 10
rules:
- description: API must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Operations must have summaries
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: Operations must have operationIds
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: Operations must have tags
  given: $.paths[*][*]
  name: operation-tags-required
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Operation summaries should start with Apache OpenMeetings
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: Servers should use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: warn
- description: Operations must have a success response
  given: $.paths[*][*].responses
  name: response-success-required
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-described
  severity: info
rules_file: rules/apache-openmeetings-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-openmeetings/refs/heads/main/rules/apache-openmeetings-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 4
slug: apache-openmeetings-spectral-rules
tags:
- Collaboration
- Video Conferencing
- Web Conferencing
- Whiteboard
- Apache
- Open Source
- Conferencing
- Spectral
- Linting
- API Governance
---
