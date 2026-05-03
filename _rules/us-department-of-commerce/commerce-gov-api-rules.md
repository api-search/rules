---
api_specs:
- filename: commerce-gov-api-openapi.yml
  format: yaml
  label: Commerce.gov API
  slug: commercegov-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-department-of-commerce/refs/heads/main/openapi/commerce-gov-api-openapi.yml
categories:
- commerce
description: Spectral linting rules defining API design standards and conventions for US Department of Commerce.
layout: rules
name: US Department of Commerce API Rules
provider_name: US Department of Commerce
provider_slug: us-department-of-commerce
rule_count: 10
rules:
- description: Operation IDs must use camelCase naming
  given: $.paths[*][*].operationId
  name: commerce-operation-ids-camel-case
  severity: warn
- description: All operations should define a 200 response
  given: $.paths[*][get,post,put,patch]
  name: commerce-response-200-present
  severity: warn
- description: API paths must use kebab-case for path segments
  given: $.paths
  name: commerce-path-kebab-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: commerce-operations-have-summaries
  severity: error
- description: All operations should have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: commerce-operations-have-tags
  severity: warn
- description: List operations should use consistent pagination parameters
  given: $.paths[*][get]
  name: commerce-pagination-params-consistent
  severity: info
- description: Successful responses should reference a schema
  given: $.paths[*][get].responses.200
  name: commerce-response-schema-defined
  severity: warn
- description: API info should include contact information
  given: $.info
  name: commerce-info-contact-present
  severity: warn
- description: API must define at least one server
  given: $
  name: commerce-servers-defined
  severity: error
- description: Tags must use Title Case naming
  given: $.tags[*].name
  name: commerce-tags-title-case
  severity: warn
rules_file: rules/commerce-gov-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-department-of-commerce/refs/heads/main/rules/commerce-gov-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: commerce-gov-api-rules
source_filename: commerce-gov-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  commerce-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming\n    message: Operation ID \"{{value}}\" should use camelCase (e.g., listNews, getBlogPost)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  commerce-response-200-present:\n    description: All operations should define a 200 response\n    message: Operation is missing a 200 OK response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  commerce-path-kebab-case:\n    description: API paths must use kebab-case for path segments\n    message: Path segment \"{{value}}\" should use kebab-case\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-zA-Z][a-zA-Z0-9_]*\\\
  \\}))*$\"\n\n  commerce-operations-have-summaries:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  commerce-operations-have-tags:\n    description: All operations should have at least one tag\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  commerce-pagination-params-consistent:\n    description: List operations should use consistent pagination parameters\n    message: List operations should support page and items_per_page parameters\n    severity: info\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  commerce-response-schema-defined:\n    description: Successful responses should reference a schema\n\
  \    message: Response 200 should define a content schema\n    severity: warn\n    given: \"$.paths[*][get].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  commerce-info-contact-present:\n    description: API info should include contact information\n    message: API info is missing contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  commerce-servers-defined:\n    description: API must define at least one server\n    message: No servers defined in the API specification\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  commerce-tags-title-case:\n    description: Tags must use Title Case naming\n    message: Tag \"{{value}}\" should use Title Case (e.g., \"News\", \"Blog Posts\")\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-department-of-commerce/refs/heads/main/rules/commerce-gov-api-rules.yml
tags:
- Commerce
- Federal Government
- Open Data
- Trade
- Economic Data
- Climate
- Standards
- Spectral
- Linting
- API Governance
---
