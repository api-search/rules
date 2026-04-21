---
categories:
- http
description: Spectral linting rules defining API design standards and conventions for Apache HttpComponents.
layout: rules
name: Apache HttpComponents API Rules
provider_name: Apache HttpComponents
provider_slug: apache-http
rule_count: 7
rules:
- description: All Apache HttpComponents API operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: http-client-operation-summary
  severity: error
- description: All Apache HttpComponents API operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: http-client-operation-id
  severity: error
- description: All Apache HttpComponents API operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: http-client-operation-tags
  severity: warn
- description: All Apache HttpComponents schema components must have a description
  given: $.components.schemas[*]
  name: http-client-schema-description
  severity: warn
- description: All Apache HttpComponents schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: http-client-property-description
  severity: info
- description: API info must include contact information
  given: $.info
  name: http-client-info-contact
  severity: warn
- description: API info must include license information
  given: $.info
  name: http-client-info-license
  severity: warn
rules_file: rules/apache-http-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-http/refs/heads/main/rules/apache-http-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 4
slug: apache-http-spectral-rules
tags:
- Apache
- HTTP Client
- Java
- Open Source
- SDK
- Spectral
- Linting
- API Governance
---
