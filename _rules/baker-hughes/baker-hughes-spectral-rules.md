---
categories:
- baker
description: Spectral linting rules defining API design standards and conventions for Baker Hughes.
layout: rules
name: Baker Hughes API Rules
provider_name: Baker Hughes
provider_slug: baker-hughes
rule_count: 15
rules:
- description: Baker Hughes APIs must include contact information.
  given: $.info
  name: baker-hughes-info-contact-required
  severity: warn
- description: API version must follow semantic versioning.
  given: $.info.version
  name: baker-hughes-info-version-semver
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: baker-hughes-path-kebab-case
  severity: warn
- description: Asset resource paths should use assetId as the path parameter.
  given: $.paths[*]~
  name: baker-hughes-path-asset-id-param
  severity: info
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: baker-hughes-operation-id-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: baker-hughes-operation-summary-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: baker-hughes-operation-tags-required
  severity: warn
- description: All Baker Hughes APIs must define security schemes.
  given: $
  name: baker-hughes-security-required
  severity: error
- description: Baker Hughes APIs should use OAuth2 for authentication.
  given: $.components.securitySchemes[*]
  name: baker-hughes-oauth2-required
  severity: warn
- description: GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: baker-hughes-response-200-required
  severity: error
- description: Error responses must reference a schema.
  given: $.paths[*][*].responses[4XX,5XX].content[*]
  name: baker-hughes-response-error-schemas
  severity: warn
- description: All named schemas must have a description.
  given: $.components.schemas[*]
  name: baker-hughes-schema-description-required
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: baker-hughes-schema-properties-descriptions
  severity: info
- description: All parameters must have descriptions.
  given: $.paths[*][*].parameters[*]
  name: baker-hughes-parameter-description-required
  severity: warn
- description: Global tags must have descriptions.
  given: $.tags[*]
  name: baker-hughes-tags-description-required
  severity: warn
rules_file: rules/baker-hughes-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/baker-hughes/refs/heads/main/rules/baker-hughes-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 10
slug: baker-hughes-spectral-rules
tags:
- Energy Technology
- Industrial IoT
- Oil And Gas
- Asset Performance Management
- Digital Energy
- Spectral
- Linting
- API Governance
---
