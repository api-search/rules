---
api_specs:
- filename: cloudmersive-virus-scan-openapi.json
  format: json
  label: Cloudmersive Virus Scan API
  slug: cloudmersive-virus-scan-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/cloudmersive/refs/heads/main/openapi/cloudmersive-virus-scan-openapi.json
categories:
- cloudmersive
description: Spectral linting rules defining API design standards and conventions for Cloudmersive.
layout: rules
name: Cloudmersive API Rules
provider_name: Cloudmersive
provider_slug: cloudmersive
rule_count: 8
rules:
- description: Each Cloudmersive product spec must declare a title.
  given: $.info
  name: cloudmersive-info-title
  severity: error
- description: Each Cloudmersive product spec must declare a description.
  given: $.info
  name: cloudmersive-info-description
  severity: warn
- description: A host (Swagger 2) or server (OpenAPI 3) must be declared.
  given: $
  name: cloudmersive-host-or-server
  severity: error
- description: Cloudmersive APIs must be served over HTTPS.
  given: $
  name: cloudmersive-https-only
  severity: error
- description: An Apikey security definition/scheme must be declared.
  given: $
  name: cloudmersive-apikey-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-summary
  severity: warn
rules_file: rules/cloudmersive-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudmersive/refs/heads/main/rules/cloudmersive-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 3
slug: cloudmersive-rules
source_filename: cloudmersive-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules applicable to all Cloudmersive product OpenAPI/Swagger\n# specs (Virus Scan, Convert, OCR, Image, NLP, Validate, Security, Spam,\n# Phishing, CDR, Fraud, DLP, Speech, Video, Currency, Barcode, Config,\n# Data Integration).\nrules:\n  cloudmersive-info-title:\n    description: Each Cloudmersive product spec must declare a title.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  cloudmersive-info-description:\n    description: Each Cloudmersive product spec must declare a description.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  cloudmersive-host-or-server:\n    description: A host (Swagger 2) or server (OpenAPI 3) must be declared.\n    severity: error\n    given: \"$\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"host\"]\n     \
  \       - required: [\"servers\"]\n\n  cloudmersive-https-only:\n    description: Cloudmersive APIs must be served over HTTPS.\n    severity: error\n    given: \"$\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - properties:\n                schemes:\n                  type: array\n                  contains:\n                    const: \"https\"\n              required: [\"schemes\"]\n            - properties:\n                servers:\n                  type: array\n                  items:\n                    properties:\n                      url:\n                        type: string\n                        pattern: \"^https://\"\n              required: [\"servers\"]\n\n  cloudmersive-apikey-security:\n    description: An Apikey security definition/scheme must be declared.\n    severity: error\n    given: \"$\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n           \
  \ - required: [\"securityDefinitions\"]\n            - properties:\n                components:\n                  required: [\"securitySchemes\"]\n              required: [\"components\"]\n\n  cloudmersive-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cloudmersive-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cloudmersive-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudmersive/refs/heads/main/rules/cloudmersive-rules.yml
tags:
- Barcodes
- Conversions
- Documents
- Image Recognition
- Natural Language
- OCR
- Processing
- Validation
- Virus Scanning
- Spectral
- Linting
- API Governance
---
