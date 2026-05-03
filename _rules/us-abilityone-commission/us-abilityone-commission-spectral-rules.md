---
api_specs:
- filename: abilityone-procurement-list-api-openapi.yml
  format: yaml
  label: AbilityOne Procurement List API
  slug: procurement-list-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-abilityone-commission/refs/heads/main/openapi/abilityone-procurement-list-api-openapi.yml
categories:
- abi
description: Spectral linting rules defining API design standards and conventions for US AbilityOne Commission.
layout: rules
name: US AbilityOne Commission API Rules
provider_name: US AbilityOne Commission
provider_slug: us-abilityone-commission
rule_count: 25
rules:
- description: API info must have a title
  given: $.info
  name: abi-info-title-present
  severity: error
- description: API info must have a description
  given: $.info
  name: abi-info-description-present
  severity: warn
- description: API info must have a version
  given: $.info
  name: abi-info-version-present
  severity: error
- description: Government APIs must have contact information
  given: $.info
  name: abi-info-contact-present
  severity: warn
- description: Must use OpenAPI 3.x
  given: $
  name: abi-openapi-version
  severity: error
- description: API must define servers
  given: $
  name: abi-servers-present
  severity: warn
- description: Server URLs should use HTTPS
  given: $.servers[*].url
  name: abi-server-url-https
  severity: warn
- description: Government APIs should use .gov domains
  given: $.servers[*].url
  name: abi-server-gov-domain
  severity: hint
- description: API must define paths
  given: $
  name: abi-paths-present
  severity: error
- description: Path segments should be lowercase
  given: $.paths[*]~
  name: abi-path-lowercase
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: abi-operation-id-present
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: abi-operation-summary-present
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: abi-operation-description-present
  severity: hint
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: abi-operation-tags-present
  severity: warn
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: abi-response-description-present
  severity: error
- description: Operations must define a 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: abi-response-success-present
  severity: error
- description: All schemas should have a description
  given: $.components.schemas[*]
  name: abi-schema-description-present
  severity: hint
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: abi-schema-properties-examples
  severity: hint
- description: NSN fields should define the correct format pattern
  given: $.paths[*][get,post].parameters[?(@.name == 'nsn')].schema
  name: abi-nsn-format-pattern
  severity: hint
- description: Status fields should use an enum to restrict values
  given: $.components.schemas[*].properties.status
  name: abi-status-enum-defined
  severity: warn
- description: Nonprofit affiliate fields should restrict to NIB or SourceAmerica
  given: $.components.schemas[*].properties.nonprofitAffiliate
  name: abi-nonprofit-affiliate-enum
  severity: warn
- description: GET operations should not have a request body
  given: $.paths[*].get
  name: abi-get-no-request-body
  severity: warn
- description: Operations should include Microcks extension for mocking
  given: $.paths[*][get,post,put,patch,delete]
  name: abi-microcks-operation-present
  severity: hint
- description: Responses should include examples for documentation
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: abi-examples-in-responses
  severity: hint
- description: All parameters should have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: abi-parameter-description-present
  severity: warn
rules_file: rules/us-abilityone-commission-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-abilityone-commission/refs/heads/main/rules/us-abilityone-commission-spectral-rules.yml
severity_counts:
  error: 7
  hint: 7
  info: 0
  warn: 11
slug: us-abilityone-commission-spectral-rules
source_filename: us-abilityone-commission-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # Info Rules\n  abi-info-title-present:\n    description: API info must have a title\n    message: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  abi-info-description-present:\n    description: API info must have a description\n    message: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  abi-info-version-present:\n    description: API info must have a version\n    message: Info object must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  abi-info-contact-present:\n    description: Government APIs must have contact information\n    message: Info object must have contact details for government APIs\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # OpenAPI Version Rules\n \
  \ abi-openapi-version:\n    description: Must use OpenAPI 3.x\n    message: OpenAPI version must be 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # Server Rules\n  abi-servers-present:\n    description: API must define servers\n    message: Servers array must be defined\n    severity: warn\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  abi-server-url-https:\n    description: Server URLs should use HTTPS\n    message: \"Server URL should use HTTPS: {{value}}\"\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  abi-server-gov-domain:\n    description: Government APIs should use .gov domains\n    message: \"Government API server should use a .gov domain: {{value}}\"\n    severity: hint\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^https://[^/]+\\\\.gov\"\n\n  # Path Rules\n  abi-paths-present:\n    description: API must define paths\n    message: Paths object must be defined and non-empty\n    severity: error\n    given: $\n    then:\n      field: paths\n      function: truthy\n\n  abi-path-lowercase:\n    description: Path segments should be lowercase\n    message: \"Path should use lowercase letters: {{value}}\"\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9/_{}.-]*$\"\n\n  # Operation Rules\n  abi-operation-id-present:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  abi-operation-summary-present:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: warn\n \
  \   given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  abi-operation-description-present:\n    description: All operations should have a description\n    message: Operation should have a description\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  abi-operation-tags-present:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  # Response Rules\n  abi-response-description-present:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  abi-response-success-present:\n  \
  \  description: Operations must define a 2xx success response\n    message: Operation must define a 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required: [\"204\"]\n\n  # Schema Rules\n  abi-schema-description-present:\n    description: All schemas should have a description\n    message: Schema should have a description\n    severity: hint\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  abi-schema-properties-examples:\n    description: Schema properties should include examples\n    message: Schema property should have an example value\n    severity: hint\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: example\n      function:\
  \ truthy\n\n  # Government-Specific Rules\n  abi-nsn-format-pattern:\n    description: NSN fields should define the correct format pattern\n    message: NSN parameter should include format pattern xxxx-xx-xxx-xxxx\n    severity: hint\n    given: $.paths[*][get,post].parameters[?(@.name == 'nsn')].schema\n    then:\n      field: pattern\n      function: truthy\n\n  abi-status-enum-defined:\n    description: Status fields should use an enum to restrict values\n    message: Status property should define an enum\n    severity: warn\n    given: $.components.schemas[*].properties.status\n    then:\n      field: enum\n      function: truthy\n\n  abi-nonprofit-affiliate-enum:\n    description: Nonprofit affiliate fields should restrict to NIB or SourceAmerica\n    message: nonprofitAffiliate should define an enum with NIB and SourceAmerica\n    severity: warn\n    given: $.components.schemas[*].properties.nonprofitAffiliate\n    then:\n      field: enum\n      function: truthy\n\n  # HTTP Method\
  \ Rules\n  abi-get-no-request-body:\n    description: GET operations should not have a request body\n    message: GET operation should not have a request body\n    severity: warn\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # Quality Rules\n  abi-microcks-operation-present:\n    description: Operations should include Microcks extension for mocking\n    message: Operation should have x-microcks-operation extension\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  abi-examples-in-responses:\n    description: Responses should include examples for documentation\n    message: Response content should include examples\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]\n    then:\n      field: examples\n      function: truthy\n\n  abi-parameter-description-present:\n    description: All parameters should have a\
  \ description\n    message: Parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-abilityone-commission/refs/heads/main/rules/us-abilityone-commission-spectral-rules.yml
tags:
- Federal Government
- Disability Employment
- Procurement
- Nonprofit
- Accessibility
- Spectral
- Linting
- API Governance
---
