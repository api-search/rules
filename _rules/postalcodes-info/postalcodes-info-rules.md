---
api_specs:
- filename: openapi.json
  format: json
  label: PostalCodes.info Postal Code Reference API
  slug: postal-code-reference-api
  spec_type: OpenAPI
  url: https://postalcodes.info/openapi.json
categories:
- postalcodes
description: Spectral linting rules defining API design standards and conventions for PostalCodes.info.
layout: rules
name: PostalCodes.info API Rules
provider_name: PostalCodes.info
provider_slug: postalcodes-info
rule_count: 11
rules:
- description: PostalCodes.info specs must keep contact details for the maintainer.
  given: $.info.contact
  name: postalcodes-info-contact-required
  severity: error
- description: PostalCodes.info data is published under the Open Database License (ODbL) 1.0.
  given: $.info.license
  name: postalcodes-info-license-odbl
  severity: warn
- description: The canonical server must point at https://postalcodes.info.
  given: $.servers[*]
  name: postalcodes-info-server-canonical-host
  severity: error
- description: Operation summaries must use Title Case to match the documentation portal.
  given: $.paths.*.*.summary
  name: postalcodes-info-operation-summary-title-case
  severity: warn
- description: operationId values should be lowerCamelCase verbs.
  given: $.paths.*.*.operationId
  name: postalcodes-info-operation-id-camel
  severity: warn
- description: Only Search, Downloads and Lookup Pages tags are sanctioned for postalcodes.info paths.
  given: $.paths.*.*.tags[*]
  name: postalcodes-info-operation-tags-allowed
  severity: warn
- description: ISO 3166-1 alpha-2 country code parameters must use a 2-letter pattern.
  given: $.paths.*.*.parameters[?(@.name=="country" && @.in=="query")].schema
  name: postalcodes-info-country-code-pattern
  severity: warn
- description: Postal codes must be modeled as strings to preserve leading zeros, spaces and punctuation.
  given: $.components.schemas.PostalRecord.properties.postal_code
  name: postalcodes-info-postal-code-is-string
  severity: error
- description: The download-token endpoint must require X-Requested-With and Referer headers.
  given: $.paths['/download-token.php'].get.parameters
  name: postalcodes-info-download-token-headers
  severity: warn
- description: The download endpoint must constrain format to csv, xlsx, json.
  given: $.paths['/download.php'].get.parameters[?(@.name=="format")].schema
  name: postalcodes-info-download-format-enum
  severity: error
- description: 200 responses should include at least one example to document the JSON shape.
  given: $.paths.*.*.responses['200'].content.application/json
  name: postalcodes-info-200-has-example
  severity: info
rules_file: rules/postalcodes-info-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/postalcodes-info/refs/heads/main/rules/postalcodes-info-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 6
slug: postalcodes-info-rules
source_filename: postalcodes-info-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\ndocumentationUrl: https://postalcodes.info/api\n\nrules:\n  # Provider identity\n  postalcodes-info-contact-required:\n    description: PostalCodes.info specs must keep contact details for the maintainer.\n    message: 'info.contact.email is required and should point to PostalCodes.info maintainer.'\n    severity: error\n    given: $.info.contact\n    then:\n      - field: email\n        function: truthy\n      - field: url\n        function: truthy\n\n  postalcodes-info-license-odbl:\n    description: PostalCodes.info data is published under the Open Database License (ODbL) 1.0.\n    message: 'info.license should reference the Open Database License (ODbL) 1.0.'\n    severity: warn\n    given: $.info.license\n    then:\n      - field: name\n        function: pattern\n        functionOptions:\n          match: '(?i)open database license|odbl'\n      - field: url\n        function: pattern\n        functionOptions:\n          match: 'opendatacommons\\\
  \\.org/licenses/odbl'\n\n  postalcodes-info-server-canonical-host:\n    description: The canonical server must point at https://postalcodes.info.\n    message: 'servers[].url must reference https://postalcodes.info.'\n    severity: error\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: '^https://postalcodes\\\\.info(/.*)?$'\n\n  # Operations and summaries\n  postalcodes-info-operation-summary-title-case:\n    description: Operation summaries must use Title Case to match the documentation portal.\n    message: 'Operation summary \"{{value}}\" should use Title Case.'\n    severity: warn\n    given: $.paths.*.*.summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z0-9][A-Za-z0-9 ,\\\\-\\\\(\\\\)/]*$'\n\n  postalcodes-info-operation-id-camel:\n    description: operationId values should be lowerCamelCase verbs.\n    message: 'operationId \"{{value}}\" should be lowerCamelCase.'\n    severity:\
  \ warn\n    given: $.paths.*.*.operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]+$'\n\n  postalcodes-info-operation-tags-allowed:\n    description: Only Search, Downloads and Lookup Pages tags are sanctioned for postalcodes.info paths.\n    message: 'Operation tag \"{{value}}\" is not one of the sanctioned tags.'\n    severity: warn\n    given: $.paths.*.*.tags[*]\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - Search\n          - Downloads\n          - Lookup Pages\n\n  # Parameters\n  postalcodes-info-country-code-pattern:\n    description: ISO 3166-1 alpha-2 country code parameters must use a 2-letter pattern.\n    message: 'country parameter must be constrained to a 2-letter ISO 3166-1 alpha-2 code.'\n    severity: warn\n    given: $.paths.*.*.parameters[?(@.name==\"country\" && @.in==\"query\")].schema\n    then:\n      field: pattern\n      function: pattern\n      functionOptions:\n\
  \        match: '\\\\^\\\\[A-Za-z\\\\]\\\\{2\\\\}\\\\$'\n\n  postalcodes-info-postal-code-is-string:\n    description: Postal codes must be modeled as strings to preserve leading zeros, spaces and punctuation.\n    message: '\"postal_code\" must be modeled as a string, not a number.'\n    severity: error\n    given: $.components.schemas.PostalRecord.properties.postal_code\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: '^string$'\n\n  # Downloads workflow\n  postalcodes-info-download-token-headers:\n    description: The download-token endpoint must require X-Requested-With and Referer headers.\n    message: 'createDownloadToken must enforce X-Requested-With and Referer same-origin headers.'\n    severity: warn\n    given: $.paths['/download-token.php'].get.parameters\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n  \
  \            name:\n                enum:\n                  - X-Requested-With\n                  - Referer\n\n  postalcodes-info-download-format-enum:\n    description: The download endpoint must constrain format to csv, xlsx, json.\n    message: 'downloadCountryDataset format parameter must be enumerated as csv | xlsx | json.'\n    severity: error\n    given: $.paths['/download.php'].get.parameters[?(@.name==\"format\")].schema\n    then:\n      field: enum\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          items:\n            type: string\n          contains:\n            enum:\n              - csv\n              - xlsx\n              - json\n\n  # Examples discipline\n  postalcodes-info-200-has-example:\n    description: 200 responses should include at least one example to document the JSON shape.\n    message: '200 response on {{path}} should include an example.'\n    severity: info\n    given: $.paths.*.*.responses['200'].content.application/json\n\
  \    then:\n      function: truthy\n      field: examples\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/postalcodes-info/refs/heads/main/rules/postalcodes-info-rules.yml
tags:
- Postal Codes
- Geocoding
- Open Data
- Address Validation
- Logistics
- Spectral
- Linting
- API Governance
---
