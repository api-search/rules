---
api_specs:
- filename: salesforce-knowledge-management-rest-api-openapi.yml
  format: yaml
  label: Salesforce Knowledge REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/salesforce-knowledge-management/refs/heads/main/openapi/salesforce-knowledge-management-rest-api-openapi.yml
categories:
- salesforce
description: Spectral linting rules defining API design standards and conventions for Salesforce Knowledge Management.
layout: rules
name: Salesforce Knowledge Management API Rules
provider_name: Salesforce Knowledge Management
provider_slug: salesforce-knowledge-management
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: salesforce-km-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: salesforce-km-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: salesforce-km-tags-title-case
  severity: warn
- description: All 200 responses must have a description
  given: $.paths[*][*].responses['200']
  name: salesforce-km-response-200-description
  severity: error
- description: API info must include contact details
  given: $.info
  name: salesforce-km-contact-required
  severity: error
- description: API info must include a version
  given: $.info
  name: salesforce-km-version-required
  severity: error
- description: API must define at least one server
  given: $
  name: salesforce-km-servers-required
  severity: error
- description: API must define security requirements
  given: $
  name: salesforce-km-security-defined
  severity: error
- description: Knowledge article PublishStatus should use defined enum values
  given: $.components.schemas.KnowledgeArticleSummary.properties.PublishStatus
  name: salesforce-km-article-status-enum
  severity: warn
rules_file: rules/salesforce-knowledge-management-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/salesforce-knowledge-management/refs/heads/main/rules/salesforce-knowledge-management-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 4
slug: salesforce-knowledge-management-rules
source_filename: salesforce-knowledge-management-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  salesforce-km-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-km-operation-id-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  salesforce-km-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  salesforce-km-response-200-description:\n    description: All 200 responses\
  \ must have a description\n    severity: error\n    given: \"$.paths[*][*].responses['200']\"\n    then:\n      field: description\n      function: truthy\n\n  salesforce-km-contact-required:\n    description: API info must include contact details\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  salesforce-km-version-required:\n    description: API info must include a version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  salesforce-km-servers-required:\n    description: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  salesforce-km-security-defined:\n    description: API must define security requirements\n    severity: error\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  salesforce-km-article-status-enum:\n    description: Knowledge article PublishStatus\
  \ should use defined enum values\n    message: \"Article PublishStatus should be one of: Online, Draft, Archived\"\n    severity: warn\n    given: \"$.components.schemas.KnowledgeArticleSummary.properties.PublishStatus\"\n    then:\n      field: enum\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/salesforce-knowledge-management/refs/heads/main/rules/salesforce-knowledge-management-rules.yml
tags:
- Articles
- CRM
- Customer Service
- Documentation
- Knowledge Management
- Support
- Spectral
- Linting
- API Governance
---
