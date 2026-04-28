---
categories:
- cloudevents
description: Spectral linting rules defining API design standards and conventions for CloudEvents.
layout: rules
name: CloudEvents API Rules
provider_name: CloudEvents
provider_slug: cloudevents
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudevents-info-contact
  severity: error
- description: API license must be declared (CloudEvents publishes under Apache-2.0).
  given: $.info
  name: cloudevents-info-license
  severity: warn
- description: CloudEvents-aligned APIs should declare an Apache-2.0 license.
  given: $.info.license.name
  name: cloudevents-info-license-apache
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudevents-server-https
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudevents-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudevents-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudevents-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudevents-error-responses
  severity: warn
- description: Subscription schemas must include the CloudEvents-required `id`, `source`, and `sink` attributes.
  given: $.components.schemas.Subscription.properties
  name: cloudevents-subscription-required-attributes
  severity: warn
rules_file: rules/cloudevents-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudevents/refs/heads/main/rules/cloudevents-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 6
slug: cloudevents-rules
tags:
- Cloud Native
- Events
- Graduated
- Interoperability
- Messaging
- Specification
- Spectral
- Linting
- API Governance
---
