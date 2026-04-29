---
categories:
- bigcommerce
description: Spectral linting rules defining API design standards and conventions for BigCommerce.
layout: rules
name: BigCommerce API Rules
provider_name: BigCommerce
provider_slug: bigcommerce
rule_count: 24
rules:
- description: API title must start with "BigCommerce"
  given: $.info.title
  name: bigcommerce-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: bigcommerce-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: bigcommerce-info-contact-present
  severity: warn
- description: API info must have a description
  given: $.info
  name: bigcommerce-info-description-present
  severity: warn
- description: Operation summaries must start with "BigCommerce"
  given: $.paths[*][*].summary
  name: bigcommerce-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: bigcommerce-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: bigcommerce-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: bigcommerce-operation-description-present
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: bigcommerce-path-kebab-case
  severity: warn
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: bigcommerce-response-200-present
  severity: error
- description: Operations must define error responses
  given: $.paths[*][post,put,patch,delete].responses
  name: bigcommerce-response-error-present
  severity: warn
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: bigcommerce-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: bigcommerce-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: bigcommerce-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: bigcommerce-security-scheme-present
  severity: error
- description: Mutating operations must declare security
  given: $.paths[*][post,put,patch,delete]
  name: bigcommerce-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: bigcommerce-tags-defined
  severity: warn
- description: Top-level tags must have a description
  given: $.tags[*]
  name: bigcommerce-tag-description-present
  severity: warn
- description: API must define servers
  given: $
  name: bigcommerce-servers-present
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: bigcommerce-server-url-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: bigcommerce-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: bigcommerce-microcks-operation-present
  severity: warn
- description: Server URLs should use store hash variable
  given: $.servers[*].url
  name: bigcommerce-store-hash-variable
  severity: warn
- description: API info must include license
  given: $.info
  name: bigcommerce-license-present
  severity: warn
rules_file: rules/bigcommerce-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bigcommerce/refs/heads/main/rules/bigcommerce-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 17
slug: bigcommerce-spectral-rules
source_yaml: "rules:\n\n  # Info rules\n  bigcommerce-info-title-prefix:\n    description: API title must start with \"BigCommerce\"\n    message: 'Info title must start with \"BigCommerce\": {{value}}'\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^BigCommerce\"\n\n  bigcommerce-info-version-present:\n    description: API info must have a version field\n    message: Info object must include a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  bigcommerce-info-contact-present:\n    description: API info must include contact details\n    message: Info object must include contact\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  bigcommerce-info-description-present:\n    description: API info must have a description\n    message: Info must include description\n    severity: warn\n    given: $.info\n    then:\n\
  \      field: description\n      function: truthy\n\n  # Operation rules\n  bigcommerce-operation-summary-prefix:\n    description: Operation summaries must start with \"BigCommerce\"\n    message: 'Operation summary must start with \"BigCommerce\": {{value}}'\n    severity: error\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^BigCommerce\"\n\n  bigcommerce-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: 'OperationId must be camelCase: {{value}}'\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  bigcommerce-operation-tags-present:\n    description: Every operation must have at least one tag\n    message: Operations must include tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  bigcommerce-operation-description-present:\n\
  \    description: Every operation must have a description\n    message: Operations must include description\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Path rules\n  bigcommerce-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: 'Path segments must be kebab-case: {{value}}'\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}._]*)+$\"\n\n  # Response rules\n  bigcommerce-response-200-present:\n    description: Every operation must define a success response\n    message: Operations must include a 200 or 201 response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  bigcommerce-response-error-present:\n  \
  \  description: Operations must define error responses\n    message: Operations should define 4xx error responses\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['400']\n            - required: ['404']\n            - required: ['422']\n\n  # Schema rules\n  bigcommerce-schema-title-present:\n    description: All schemas must have a title\n    message: Schemas must include title\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\n  bigcommerce-schema-description-present:\n    description: All schemas must have a description\n    message: Schemas must include description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  bigcommerce-schema-properties-described:\n    description:\
  \ Schema properties must have descriptions\n    message: Schema properties must include description\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Security rules\n  bigcommerce-security-scheme-present:\n    description: API must define at least one security scheme\n    message: Components must include securitySchemes\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  bigcommerce-operation-security-present:\n    description: Mutating operations must declare security\n    message: POST/PUT/PATCH/DELETE operations must include security\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # Tag rules\n  bigcommerce-tags-defined:\n    description: All tags used in operations must be defined at top level\n    message: Tags must be defined in the global\
  \ tags section\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n\n  bigcommerce-tag-description-present:\n    description: Top-level tags must have a description\n    message: Tags must include a description\n    severity: warn\n    given: \"$.tags[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Server rules\n  bigcommerce-servers-present:\n    description: API must define servers\n    message: Servers array must be present and non-empty\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  bigcommerce-server-url-https:\n    description: Server URLs must use HTTPS\n    message: 'Server URL must use HTTPS: {{value}}'\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Examples rules\n  bigcommerce-operation-examples-present:\n    description: Responses with content should include examples\n\
  \    message: Response content should include examples\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content[*]\"\n    then:\n      field: examples\n      function: truthy\n\n  bigcommerce-microcks-operation-present:\n    description: Every operation must include x-microcks-operation extension\n    message: Operations must include x-microcks-operation\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  # Store hash rules\n  bigcommerce-store-hash-variable:\n    description: Server URLs should use store hash variable\n    message: Server URL should include store_hash variable\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\\\\{store_hash\\\\}\"\n\n  # License rules\n  bigcommerce-license-present:\n    description: API info must include license\n    message: Info must include license\n    severity: warn\n    given: \"\
  $.info\"\n    then:\n      field: license\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/bigcommerce/refs/heads/main/rules/bigcommerce-spectral-rules.yml
tags:
- E-Commerce
- Retail
- Catalog
- Orders
- Checkout
- Payments
- SaaS
- Spectral
- Linting
- API Governance
---
