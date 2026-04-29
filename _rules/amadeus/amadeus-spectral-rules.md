---
categories:
- amadeus
description: Spectral linting rules defining API design standards and conventions for Amadeus.
layout: rules
name: Amadeus API Rules
provider_name: Amadeus
provider_slug: amadeus
rule_count: 15
rules:
- description: API info must have a title field.
  given: $.info
  name: amadeus-info-title-required
  severity: error
- description: API info must have a description.
  given: $.info
  name: amadeus-info-description-required
  severity: error
- description: API info must have a version.
  given: $.info
  name: amadeus-info-version-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-summary-required
  severity: error
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-description-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-tags-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-operationid-required
  severity: error
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: amadeus-parameter-description-required
  severity: warn
- description: All GET operations must have a 200 response.
  given: $.paths[*].get
  name: amadeus-response-200-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: amadeus-response-description-required
  severity: warn
- description: API should define bearer security scheme.
  given: $.components.securitySchemes
  name: amadeus-security-bearer-defined
  severity: warn
- description: Schemas should have descriptions.
  given: $.components.schemas[*]
  name: amadeus-schema-description
  severity: info
- description: API paths should use kebab-case.
  given: $.paths
  name: amadeus-paths-kebab-case
  severity: warn
- description: API info should include contact information.
  given: $.info
  name: amadeus-contact-required
  severity: info
- description: API must define at least one server.
  given: $
  name: amadeus-servers-required
  severity: error
rules_file: rules/amadeus-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/amadeus/refs/heads/main/rules/amadeus-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 5
slug: amadeus-spectral-rules
source_yaml: "extends:\n- - spectral:oas\n  - all\nrules:\n  amadeus-info-title-required:\n    description: API info must have a title field.\n    message: Info object must include a title.\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n  amadeus-info-description-required:\n    description: API info must have a description.\n    message: Info object must include a description.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n  amadeus-info-version-required:\n    description: API info must have a version.\n    message: Info object must include a version.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n  amadeus-operation-summary-required:\n    description: All operations must have a summary.\n    message: Operation must include a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n\
  \      function: truthy\n  amadeus-operation-description-required:\n    description: All operations should have a description.\n    message: Operation should include a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n  amadeus-operation-tags-required:\n    description: All operations must have at least one tag.\n    message: Operation must include at least one tag.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n  amadeus-operation-operationid-required:\n    description: All operations must have an operationId.\n    message: Operation must include an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n  amadeus-parameter-description-required:\n    description: All parameters must have a description.\n    message: Parameter\
  \ must include a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n  amadeus-response-200-required:\n    description: All GET operations must have a 200 response.\n    message: GET operation must include a 200 response.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: responses.200\n      function: truthy\n  amadeus-response-description-required:\n    description: All responses must have a description.\n    message: Response must include a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n  amadeus-security-bearer-defined:\n    description: API should define bearer security scheme.\n    message: API should include BearerAuth security scheme.\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      field: BearerAuth\n      function:\
  \ truthy\n  amadeus-schema-description:\n    description: Schemas should have descriptions.\n    message: Schema component should include a description.\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n  amadeus-paths-kebab-case:\n    description: API paths should use kebab-case.\n    message: Path must use kebab-case.\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: ^(/[a-z0-9{}-]+)+$\n  amadeus-contact-required:\n    description: API info should include contact information.\n    message: Info object should include contact details.\n    severity: info\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n  amadeus-servers-required:\n    description: API must define at least one server.\n    message: API must include a servers array.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/amadeus/refs/heads/main/rules/amadeus-spectral-rules.yml
tags:
- Airlines
- Aviation
- Booking
- Destinations
- Flights
- Hospitality
- Hotels
- Market Insights
- Tourism
- Transfers
- Travel
- Spectral
- Linting
- API Governance
---
