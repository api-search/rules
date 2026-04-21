---
categories:
- info
- operation
- pagination
- parameter
- paths
- response
- servers
description: Spectral linting rules defining API design standards and conventions for Apify.
layout: rules
name: Apify API Rules
provider_name: Apify
provider_slug: apify
rule_count: 11
rules:
- description: API title must start with 'Apify'.
  given: $.info
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Operation summaries must start with 'Apify'.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-camelcase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Paths must include API version /v2/ prefix.
  given: $.paths
  name: paths-v2-version
  severity: info
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Collection endpoints should use limit/offset pagination.
  given: $.paths[*].get.parameters[*]
  name: pagination-limit-offset
  severity: info
rules_file: rules/apify-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apify/refs/heads/main/rules/apify-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 5
slug: apify-spectral-rules
tags:
- Actors
- Browser Automation
- Crawling
- Data Aggregation
- Data Extraction
- Web Automation
- Web Scraping
- Spectral
- Linting
- API Governance
---
