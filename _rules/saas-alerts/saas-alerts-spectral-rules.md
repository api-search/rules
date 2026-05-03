---
api_specs:
- filename: saas-alerts-openapi.yml
  format: yaml
  label: SaaS Alerts API
  slug: saas-alerts
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/saas-alerts/refs/heads/main/openapi/saas-alerts-openapi.yml
categories:
- saas
description: Spectral linting rules defining API design standards and conventions for SaaS Alerts.
layout: rules
name: SaaS Alerts API Rules
provider_name: SaaS Alerts
provider_slug: saas-alerts
rule_count: 9
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: saas-alerts-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: saas-alerts-tags-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: saas-alerts-operation-ids-camel-case
  severity: warn
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: saas-alerts-security-scheme-required
  severity: error
- description: List operations should support pagination with pageSize and page parameters
  given: $.paths[*][get]
  name: saas-alerts-pagination-params
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: saas-alerts-parameters-have-descriptions
  severity: warn
- description: alertStatus parameters must use defined enum values
  given: $.paths[*][*].parameters[?(@.name == 'alertStatus')].schema
  name: saas-alerts-enum-alert-status-values
  severity: error
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: saas-alerts-paths-kebab-case
  severity: warn
- description: Component schema names must use PascalCase
  given: $.components.schemas[*]~
  name: saas-alerts-schema-names-pascal-case
  severity: warn
rules_file: rules/saas-alerts-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/saas-alerts/refs/heads/main/rules/saas-alerts-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 7
slug: saas-alerts-spectral-rules
source_filename: saas-alerts-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  saas-alerts-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  saas-alerts-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  saas-alerts-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[a-z][a-zA-Z0-9]*$\"\n\n  saas-alerts-security-scheme-required:\n    description: All operations must define security requirements\n    message: \"Operation must define security requirements (API key authentication required)\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  saas-alerts-pagination-params:\n    description: List operations should support pagination with pageSize and page parameters\n    message: \"GET list operations should include pageSize and page query parameters\"\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  saas-alerts-parameters-have-descriptions:\n    description: All parameters must have descriptions\n    message: \"Parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  saas-alerts-enum-alert-status-values:\n    description: alertStatus parameters must use defined enum values\n    message: \"alertStatus must be one of: low, medium, critical\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name == 'alertStatus')].schema\"\n    then:\n      field: enum\n      function: truthy\n\n  saas-alerts-paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segments must use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"[A-Z_]\"\n\n  saas-alerts-schema-names-pascal-case:\n    description: Component schema names must use PascalCase\n    message: \"Schema name must use PascalCase\"\n    severity: warn\n    given: \"$.components.schemas[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/saas-alerts/refs/heads/main/rules/saas-alerts-spectral-rules.yml
tags:
- MSP
- SaaS Security
- Security Monitoring
- Threat Detection
- Microsoft 365
- Google Workspace
- MSSP
- Spectral
- Linting
- API Governance
---
