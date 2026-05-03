---
api_specs:
- filename: usadf-grants-api-openapi.yml
  format: yaml
  label: USADF Grants Data API
  slug: grants-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-african-development-foundation/refs/heads/main/openapi/usadf-grants-api-openapi.yml
- filename: usadf-grant-opportunities-api-openapi.yml
  format: yaml
  label: USADF Grant Opportunities API
  slug: grant-opportunities-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-african-development-foundation/refs/heads/main/openapi/usadf-grant-opportunities-api-openapi.yml
categories:
- usadf
description: Spectral linting rules defining API design standards and conventions for US African Development Foundation.
layout: rules
name: US African Development Foundation API Rules
provider_name: US African Development Foundation
provider_slug: us-african-development-foundation
rule_count: 25
rules:
- description: API info must have a title
  given: $.info
  name: usadf-info-title-present
  severity: error
- description: API info must have a description
  given: $.info
  name: usadf-info-description-present
  severity: warn
- description: API info must have a version
  given: $.info
  name: usadf-info-version-present
  severity: error
- description: Government APIs must have contact information
  given: $.info
  name: usadf-info-contact-present
  severity: warn
- description: Must use OpenAPI 3.x
  given: $
  name: usadf-openapi-version
  severity: error
- description: API must define servers
  given: $
  name: usadf-servers-present
  severity: warn
- description: Server URLs should use HTTPS
  given: $.servers[*].url
  name: usadf-server-url-https
  severity: warn
- description: API must define paths
  given: $
  name: usadf-paths-present
  severity: error
- description: Path segments should use kebab-case or underscores
  given: $.paths[*]~
  name: usadf-path-kebab-case
  severity: hint
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: usadf-operation-id-present
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: usadf-operation-summary-present
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: usadf-operation-description-present
  severity: hint
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: usadf-operation-tags-present
  severity: warn
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: usadf-response-description-present
  severity: error
- description: Operations must define a 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: usadf-response-success-present
  severity: error
- description: All schemas should have a description
  given: $.components.schemas[*]
  name: usadf-schema-description-present
  severity: hint
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: usadf-schema-properties-examples
  severity: hint
- description: Award schemas should define total obligation or award amount
  given: $.components.schemas.Award.properties
  name: usadf-award-amount-defined
  severity: hint
- description: Grant opportunity schemas must define open and close dates
  given: $.components.schemas.Opportunity.properties
  name: usadf-opportunity-dates-defined
  severity: warn
- description: Grant opportunity status should use an enum
  given: $.components.schemas.Opportunity.properties.oppStatus
  name: usadf-opportunity-status-enum
  severity: warn
- description: Award category should use an enum
  given: $.components.schemas.Award.properties.category
  name: usadf-award-category-enum
  severity: hint
- description: GET operations should not have a request body
  given: $.paths[*].get
  name: usadf-get-no-request-body
  severity: warn
- description: Operations should include Microcks extension for mocking
  given: $.paths[*][get,post,put,patch,delete]
  name: usadf-microcks-operation-present
  severity: hint
- description: Responses should include examples
  given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]
  name: usadf-examples-in-responses
  severity: hint
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: usadf-parameter-description
  severity: warn
rules_file: rules/us-african-development-foundation-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-african-development-foundation/refs/heads/main/rules/us-african-development-foundation-spectral-rules.yml
severity_counts:
  error: 7
  hint: 8
  info: 0
  warn: 10
slug: us-african-development-foundation-spectral-rules
source_filename: us-african-development-foundation-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # Info Rules\n  usadf-info-title-present:\n    description: API info must have a title\n    message: Info object must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  usadf-info-description-present:\n    description: API info must have a description\n    message: Info object must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  usadf-info-version-present:\n    description: API info must have a version\n    message: Info object must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  usadf-info-contact-present:\n    description: Government APIs must have contact information\n    message: Info object must include contact details for government APIs\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # OpenAPI Version\
  \ Rules\n  usadf-openapi-version:\n    description: Must use OpenAPI 3.x\n    message: OpenAPI version must be 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # Server Rules\n  usadf-servers-present:\n    description: API must define servers\n    message: Servers array must be defined\n    severity: warn\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  usadf-server-url-https:\n    description: Server URLs should use HTTPS\n    message: \"Server URL should use HTTPS: {{value}}\"\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Path Rules\n  usadf-paths-present:\n    description: API must define paths\n    message: Paths object must be defined and non-empty\n    severity: error\n    given: $\n    then:\n      field: paths\n      function: truthy\n\n  usadf-path-kebab-case:\n\
  \    description: Path segments should use kebab-case or underscores\n    message: \"Path should use lowercase letters: {{value}}\"\n    severity: hint\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9/_{}.-]*$\"\n\n  # Operation Rules\n  usadf-operation-id-present:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  usadf-operation-summary-present:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  usadf-operation-description-present:\n    description: All operations should have a description\n    message: Operation should have a description\n    severity: hint\n\
  \    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  usadf-operation-tags-present:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  # Response Rules\n  usadf-response-description-present:\n    description: All responses must have a description\n    message: Response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  usadf-response-success-present:\n    description: Operations must define a 2xx success response\n    message: Operation must define a 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  # Schema Rules\n  usadf-schema-description-present:\n    description: All schemas should have a description\n    message: Schema should have a description\n    severity: hint\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  usadf-schema-properties-examples:\n    description: Schema properties should include examples\n    message: Schema property should have an example value\n    severity: hint\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: example\n      function: truthy\n\n  # Government Grant-Specific Rules\n  usadf-award-amount-defined:\n    description: Award schemas should define total obligation or award amount\n    message: Award schema should define total_obligation or estimatedTotalProgramFunding\n    severity: hint\n    given: $.components.schemas.Award.properties\n    then:\n    \
  \  field: total_obligation\n      function: truthy\n\n  usadf-opportunity-dates-defined:\n    description: Grant opportunity schemas must define open and close dates\n    message: Opportunity schema should define openDate and closeDate\n    severity: warn\n    given: $.components.schemas.Opportunity.properties\n    then:\n      field: closeDate\n      function: truthy\n\n  usadf-opportunity-status-enum:\n    description: Grant opportunity status should use an enum\n    message: Opportunity status should define an enum\n    severity: warn\n    given: $.components.schemas.Opportunity.properties.oppStatus\n    then:\n      field: enum\n      function: truthy\n\n  usadf-award-category-enum:\n    description: Award category should use an enum\n    message: Award category should define an enum of valid values\n    severity: hint\n    given: $.components.schemas.Award.properties.category\n    then:\n      field: enum\n      function: truthy\n\n  # HTTP Method Rules\n  usadf-get-no-request-body:\n\
  \    description: GET operations should not have a request body\n    message: GET operation should not have a request body\n    severity: warn\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # Quality Rules\n  usadf-microcks-operation-present:\n    description: Operations should include Microcks extension for mocking\n    message: Operation should have x-microcks-operation extension\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  usadf-examples-in-responses:\n    description: Responses should include examples\n    message: Response content should include examples\n    severity: hint\n    given: $.paths[*][get,post,put,patch,delete].responses[*].content[*]\n    then:\n      field: examples\n      function: truthy\n\n  usadf-parameter-description:\n    description: Parameters should have descriptions\n    message: Parameter should have a description\n\
  \    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-african-development-foundation/refs/heads/main/rules/us-african-development-foundation-spectral-rules.yml
tags:
- Federal Government
- International Development
- Africa
- Grants
- Nonprofit
- Economic Development
- Spectral
- Linting
- API Governance
---
