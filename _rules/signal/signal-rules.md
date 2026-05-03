---
api_specs:
- filename: signal-server-openapi.yml
  format: yaml
  label: Signal Server
  slug: signal-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/openapi/signal-server-openapi.yml
categories:
- signal
description: Spectral linting rules defining API design standards and conventions for Signal.
layout: rules
name: Signal API Rules
provider_name: Signal
provider_slug: signal
rule_count: 8
rules:
- description: Signal Server API uses Basic authentication with phone number credentials
  given: $.components.securitySchemes[*]
  name: signal-basic-auth-required
  severity: warn
- description: Signal Server path parameters should follow consistent naming
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: signal-path-param-naming
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: signal-operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][*]
  name: signal-operation-summary-required
  severity: error
- description: DELETE operations should return 204
  given: $.paths[*].delete.responses
  name: signal-delete-returns-204
  severity: warn
- description: Pre-key upload operations should use PUT method
  given: $.paths[?(@property =~ /keys/)][put]
  name: signal-prekey-operations-use-put
  severity: hint
- description: Operations should define 401 unauthorized response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: signal-auth-error-response
  severity: warn
- description: Cryptographic key fields should document Base64 encoding
  given: $.components.schemas[*].properties[?(@.description =~ /base64/i)]
  name: signal-base64-key-format
  severity: hint
rules_file: rules/signal-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/rules/signal-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 4
slug: signal-rules
source_filename: signal-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Signal Server uses Basic auth (username:password where username=number, password=signaling key)\n  signal-basic-auth-required:\n    description: Signal Server API uses Basic authentication with phone number credentials\n    message: Signal Server API should use http basic auth scheme\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: scheme\n      function: enumeration\n      functionOptions:\n        values:\n          - basic\n          - bearer\n\n  # Signal uses phone number or UUID as primary identifier in paths\n  signal-path-param-naming:\n    description: Signal Server path parameters should follow consistent naming\n    message: Path parameters should use consistent Signal Server naming conventions\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^(deviceId|sourceDeviceId|destinationServiceId|usernameHash|recipientUUID|attachmentId|packId|stickerNum|messageGuid|keyId)$\"\
  \n\n  # All Signal API operations must have operationId\n  signal-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # All operations must have a summary in Title Case\n  signal-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation is missing a summary\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Signal Server returns 204 for message sending (no content)\n  signal-delete-returns-204:\n    description: DELETE operations should return 204\n    message: DELETE operations should define a 204 No Content response\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: \"204\"\n      function: truthy\n\n  # Pre-key upload operations\
  \ should use PUT method\n  signal-prekey-operations-use-put:\n    description: Pre-key upload operations should use PUT method\n    message: Pre-key upload should use PUT (idempotent key upload)\n    severity: hint\n    given: \"$.paths[?(@property =~ /keys/)][put]\"\n    then:\n      function: truthy\n\n  # All responses must define at minimum a 401 error\n  signal-auth-error-response:\n    description: Operations should define 401 unauthorized response\n    message: Operation should define a 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # API key base64 parameters should document encoding\n  signal-base64-key-format:\n    description: Cryptographic key fields should document Base64 encoding\n    message: Cryptographic key properties should specify Base64 pattern\n    severity: hint\n    given: \"$.components.schemas[*].properties[?(@.description =~ /base64/i)]\"\
  \n    then:\n      field: pattern\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/signal/refs/heads/main/rules/signal-rules.yml
tags:
- Encryption
- Messaging
- Security
- Cryptography
- Open Source
- Privacy
- Spectral
- Linting
- API Governance
---
